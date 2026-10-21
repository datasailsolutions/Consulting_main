# Auto Deploy

Every push to `main` runs `.github/workflows/deploy.yml`, which copies the public
site files (`*.html`, `css/`, `js/`, `assets/`) to the Lightsail server with
`rsync --delete`. Nginx serves them directly. No build step, no PM2.

You can also run it manually from GitHub: **Actions → Deploy to Lightsail → Run workflow**.

## One-time server setup

SSH to the Lightsail box (`ssh sentrysail`), then:

```bash
# Web root owned by the deploy user
sudo mkdir -p /var/www/datasailsolutions
sudo chown ubuntu:ubuntu /var/www/datasailsolutions

# Dedicated deploy key (run on your own machine, not the server)
ssh-keygen -t ed25519 -C "github-deploy-datasail" -f datasail_deploy -N ""
# Append datasail_deploy.pub to ~/.ssh/authorized_keys on the server

# Nginx site
sudo cp deploy/nginx-datasailsolutions.conf /etc/nginx/sites-available/datasailsolutions
sudo ln -s /etc/nginx/sites-available/datasailsolutions /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
sudo certbot --nginx -d datasailsolutions.com -d www.datasailsolutions.com
```

In Cloudflare, point `datasailsolutions.com` and `www` A records at the Lightsail IP.

## GitHub secrets

Repo → **Settings → Secrets and variables → Actions** (or the `production` environment):

| Secret | Value |
| --- | --- |
| `DEPLOY_HOST` | Lightsail public IP |
| `DEPLOY_USER` | `ubuntu` |
| `DEPLOY_SSH_KEY` | Contents of the private key `datasail_deploy` |
| `DEPLOY_PATH` | Optional. Defaults to `/var/www/datasailsolutions` |
| `DEPLOY_KNOWN_HOSTS` | Optional but recommended. Output of `ssh-keyscan -H <ip>` |
