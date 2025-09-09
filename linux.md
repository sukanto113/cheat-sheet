## 🔍 Check disk usage per directory
```sh
sudo du -h --max-depth=1 / | sort -hr | head -n 20
```

## Make a .sh executable 
```sh
chmod +x your-script.sh
```
## create swpon
```sh
sudo fallocate -l 8G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

## check free ram
```sh
free -h
swapon --show
```

## Chear swap and cache
```sh
sudo sync
sudo swapoff -a && sudo swapon -a
echo 3 | sudo tee /proc/sys/vm/drop_caches
```