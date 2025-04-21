
```sh
apt update && apt install -y chromium
```

## required to run headless:false
```sh
sudo apt install -y xvfb x11-xkb-utils x11-utils x11-common xserver-xorg

pkill Xvfb
Xvfb :99 -screen 0 1920x1080x24 &
export DISPLAY=:99
```

```js
const puppeteer = require("puppeteer");
const browser = await puppeteer.launch({
  headless: false,
  executablePath: "/snap/bin/chromium",
  args: ["--no-sandbox", "--disable-setuid-sandbox"],
});
```
