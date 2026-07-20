```ts
// filter-test-output.ts

const NEWLINE = 10; // '\n'
const DOT = 46; // '.'

let pending: Uint8Array | null = null;

for await (const chunk of Bun.stdin.stream()) {
  let buf = chunk;
  if (pending) {
    const merged = new Uint8Array(pending.length + buf.length);
    merged.set(pending);
    merged.set(buf, pending.length);
    buf = merged;
    pending = null;
  }

  let start = 0;
  for (let i = 0; i < buf.length; i++) {
    if (buf[i] === NEWLINE) {
      if (buf[start] !== DOT) {
        process.stdout.write(buf.subarray(start, i + 1));
      }
      start = i + 1;
    }
  }

  if (start < buf.length) {
    pending = buf.subarray(start);
  }
}

if (pending && pending.length > 0 && pending[0] !== DOT) {
  process.stdout.write(pending);
}
export {};
```

### clean test run output
```sh
"test:filter": "bun test --reporter=dot 2>&1 | bun filter-test-output.ts",
"test:watch": "bun test --watch --reporter=dot 2>&1 | bun filter-test-output.ts"

bun test --watch --reporter=dot 2>&1 | Select-String -Pattern "^\."  -NotMatch
bun test 2>&1 | Select-Object -Last 1
npm run test:unit 2>&1 | Select-Object -Last 5
npm run test 2>&1 | Select-Object -Last 5
```