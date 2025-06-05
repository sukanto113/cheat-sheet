pm2 start ./ecosystem.config.js
pm2 startup
pm2 save
systemctl restart pm2-root