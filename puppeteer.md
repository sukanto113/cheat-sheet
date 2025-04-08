
```sh
apt update && apt install -y chromium
```

```js
const puppeteer = require("puppeteer");
const browser = await puppeteer.launch({
  executablePath: "/snap/bin/chromium",
  args: ["--no-sandbox", "--disable-setuid-sandbox"],
});
```
