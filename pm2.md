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
pm2 save
pm2 startup 
systemctl restart pm2-root

# Step 1: Apply new config
pm2 reload ecosystem.config.js

# increast restart timeout

sudo systemctl edit pm2-root
```
[Service]
TimeoutStopSec=200
TimeoutStartSec=200
Restart=always
RestartSec=5
```

sudo systemctl daemon-reload
sudo systemctl restart pm2-root
pm2 list

