```sh
apt update && apt install -y chromium
```

apt update && apt install -y chromium-browser

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
  userDataDir: "puppeteer_dev_chrome_profile-V0ugOW",
  executablePath: "/usr/bin/chromium-browser",
  // executablePath: "/snap/bin/chromium",
  args: ["--no-sandbox", "--disable-setuid-sandbox"],
});
```

// userDataDir:"/tmp/snap-private-tmp/snap.chromium/tmp",

## check cache size

df -h

du -sh /root/.cache/puppeteer

sudo du -h --max-depth=1 /tmp/snap-private-tmp/snap.chromium/tmp/ | sort -hr | head -n 20

## delete cache

rm -rf /tmp/puppeteer-profile-\*

/tmp/snap-private-tmp/snap.chromium/tmp/

ls /tmp/snap-private-tmp/snap.chromium/

find /srv/az/files -type f -mmin +60 -delete

find /tmp/snap-private-tmp/snap.chromium/tmp/ -type d -mmin +30 -exec rm -rf {} +

du -sh /tmp
