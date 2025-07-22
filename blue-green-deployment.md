ln -sfn my-app-blue my-app


# Update Process (Zero Downtime)

```sh
#!/bin/bash

set -e  # Exit immediately on any command failure

cd /var/www

ACTIVE=$(readlink my-app | awk -F'/' '{print $NF}')
INACTIVE="my-app-green"
if [ "$ACTIVE" = "my-app-green" ]; then INACTIVE="my-app-blue"; fi

echo "Deploying to: $INACTIVE"

cd $INACTIVE
git fetch origin
git reset --hard origin/main

npm install
npm run build  # if this fails, script will exit before switching symlink

# Only reached if build succeeds
ln -sfn /var/www/$INACTIVE /var/www/my-app

pm2 reload next-app

echo "✅ Deployment complete to $INACTIVE"
```