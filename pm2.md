pm2 start ./ecosystem.config.js
pm2 startup
pm2 save
systemctl restart pm2-root


# Full PM2 Ecosystem Reset Commands:
## Stop all PM2 processes
pm2 stop all

## Delete all PM2 processes
pm2 delete all

## Clear saved process list
pm2 save --force


## reset ecosystem.config.js
pm2 stop all
pm2 delete all
pm2 save --force
pm2 start ./ecosystem.config.js
pm2 startup
pm2 save
systemctl restart pm2-root


# Quick patch for Next.js to emit ready

```js
// start-server.js
const { spawn } = require("child_process");

const proc = spawn("npx", ["next", "start"], {
  stdio: ["inherit", "inherit", "inherit"],
});

proc.on("spawn", () => {
  // Fake delay if needed (e.g., to wait for "ready" log)
  setTimeout(() => {
    if (process.send) process.send("ready");
  }, 4000);
});
```

```js
{
  script: "start-server.js",
  wait_ready: true,
  listen_timeout: 8000,
  kill_timeout: 8000,
  exec_mode: "cluster",
  instances: 1
}
```