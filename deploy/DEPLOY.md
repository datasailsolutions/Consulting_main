# Auto Deploy

Every push to `main` runs `.github/workflows/deploy.yml`, which copies the public
site files (`*.html`, `css/`, `js/`, `assets/`) to the Lightsail server with
`rsync --delete`. Nginx serves them directly. No build step, no PM2.

You can also run it manually from GitHub: **Actions → Deploy to Lightsail → Run workflow**.

## Server

- Box: `sentrysail` (54.191.209.220). DNS for `datasailsolutions.com` and `www`
  points straight at it.
- Web root: `/var/www/datasail-site` (owned by `ubuntu`).
- Nginx site: `/etc/nginx/sites-available/datasailsolutions.com`, TLS via certbot.
  `deploy/nginx-datasailsolutions.conf` mirrors it.

`rsync --delete` removes anything in the web root that isn't a public site file,
including any old git checkout (`.git`, `AGENTS.md`, `README.md`, `dev-server.js`).
Don't `git pull` on the server anymore; push to `main` instead.

## One-time setup

```bash
# Dedicated deploy key (run on your own machine, not the server)
ssh-keygen -t ed25519 -C "github-deploy-datasail" -f datasail_deploy -N ""
# Append datasail_deploy.pub to /home/ubuntu/.ssh/authorized_keys on sentrysail
```

## GitHub secrets

Repo → **Settings → Secrets and variables → Actions** (or the `production` environment):

| Secret | Value |
| --- | --- |
| `DEPLOY_HOST` | `54.191.209.220` |
| `DEPLOY_USER` | `ubuntu` |
| `DEPLOY_SSH_KEY` | Contents of the private key `datasail_deploy` |
| `DEPLOY_PATH` | Optional. Defaults to `/var/www/datasail-site` |
| `DEPLOY_KNOWN_HOSTS` | Optional but recommended. Output of `ssh-keyscan -H 54.191.209.220` |
