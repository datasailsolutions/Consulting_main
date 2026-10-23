# DataSail Solutions Website - Codex Context

## Project

Static marketing website for DataSail Solutions.

Local project root:

```text
C:\Codex Projects\DataSailSolutions\datasail-site
```

GitHub repo:

```text
https://github.com/datasailsolutions/Consulting_main.git
```

Current branch:

```text
main
```

## Company Positioning

DataSail Solutions is an AI-enabled business technology consultancy.

Core positioning:

- Helps businesses improve decision-making and productivity.
- Builds custom tools, dashboards, workflows, and automations.
- Analyzes data and creates decision-support systems.
- Educates leaders and teams on practical AI adoption.
- Uses AI as part of the workbench, but does not force every solution to be AI-powered.
- Veteran-owned is a trust signal, not the main headline.

Preferred messaging tone:

- Practical, clear, trustworthy, modern.
- AI-forward but not hype-driven.
- Business-first and outcome-oriented.
- Avoid sounding like the company only builds AI products.

Useful phrasing:

```text
Build better tools. Make better decisions. Work smarter.
```

```text
We use AI where it creates value, and sound engineering where it matters most.
```

## Site Structure

Plain static site. No build step required.

Files:

- `index.html` - homepage
- `services.html` - service detail page
- `about.html` - company/founder page
- `contact.html` - contact page
- `css/styles.css` - shared styling
- `js/main.js` - mobile nav behavior
- `assets/hero-pattern.svg` - homepage hero visual
- `assets/mike-locy.png` - founder photo
- `assets/datasail-logo-option-5.png` - generated concept crop
- `assets/datasail-mark-option-5.png` - transparent mark used in header/footer
- `dev-server.js` - tiny local static server
- `.github/workflows/deploy.yml` - auto-deploy to Lightsail on push to `main`
- `deploy/` - deploy docs and the mirrored nginx config

## Design Direction

Current design direction:

- Modern consulting site
- Calm, confident, and practical
- Deep navy/teal with copper/gold accent
- Maritime/data motif without nautical kitsch
- Clean sections, restrained cards, strong typography

Logo direction:

- User chose option #5 from a generated six-logo concept sheet.
- The full square logo looked pasted in, so the site now uses an extracted transparent icon mark plus live text.
- Header/footer use `assets/datasail-mark-option-5.png` and text `DataSail Solutions`.
- Footer mark has a light chip behind it for contrast on the dark footer.

## Founder/About Notes

Founder section uses Mike Locy's existing site/about content, refined:

- Navy veteran
- Product leader
- More than 20 years of experience
- Helps technology companies solve customer problems, create differentiated solutions, and drive business results
- Partners with businesses to improve productivity, apply AI/automation, and deliver better customer experiences

Avoid customer-facing language that explains internal positioning strategy. For example, do not say that veteran-owned "does not define the work"; instead use direct customer-facing trust language.

## Local Preview

Run:

```powershell
node dev-server.js
```

Open:

```text
http://127.0.0.1:4173/
```

The server can bind to another host with:

```powershell
$env:HOST='0.0.0.0'; node dev-server.js
```

However, phone access only works from the same Wi-Fi unless using a public tunnel or deployed server.

## Hosting & Deploy (current as of 2026-10-22)

**Push to `main` = live.** `.github/workflows/deploy.yml` rsyncs the public files
(`*.html` in the root, `css/`, `js/`, `assets/`) to the server with `--delete`.
Takes about a minute. Can also be run manually: Actions → Deploy to Lightsail → Run workflow.
Full setup details: `deploy/DEPLOY.md`.

- Server: `sentrysail` Lightsail box, `54.191.209.220` (`ssh sentrysail`). Business box; shared with the SentrySail app.
- DNS: `datasailsolutions.com` and `www` A records point straight at the box (not proxied).
- Web root: `/var/www/datasail-site`. Plain static files, no git checkout, no PM2.
- Nginx: `/etc/nginx/sites-available/datasailsolutions.com`, TLS via certbot.
  `deploy/nginx-datasailsolutions.conf` mirrors it. Keep the two in sync.
- Deploy auth: key `~/.ssh/datasail_deploy` on Mikel's PC, logs in as `ubuntu`.
  Repo secrets `DEPLOY_HOST`, `DEPLOY_USER`, `DEPLOY_SSH_KEY`, `DEPLOY_KNOWN_HOSTS` are set.
  `DEPLOY_PATH` is unset (the workflow defaults to `/var/www/datasail-site`).

Rules:

- **Do not `git pull` on the server** or copy the repo into the web root. That once exposed
  `/.git/` publicly. Only the public files get deployed.
- Anything new that should be public must live in a root `*.html` file or in `css/`, `js/`, or `assets/`.
  Other files (`AGENTS.md`, `deploy/`, `design-snapshots/`, `dev-server.js`) are never deployed.
- Nginx denies dotfiles (`location ~ /\. { deny all; }`). Keep that block.
- Editing nginx over SSH: shell quoting strips the backslash in `/\.` and turns the rule into
  "deny everything" (this caused an outage). Edit `deploy/nginx-datasailsolutions.conf` locally,
  `scp` it up, then `grep -F 'location ~ /\. {'` it, then `nginx -t`, then reload. Back up the live file to `/root/` first.
  From Git Bash on Windows, set `MSYS_NO_PATHCONV=1` for ssh/scp.
- After any deploy or nginx change, check that `https://datasailsolutions.com/` returns 200 and `/.git/HEAD` returns 403.
- `gh` is not logged in on Mikel's PC. For GitHub API calls (secrets, workflow runs), use the token from
  `git credential fill` (host github.com, username `datasailsolutions`). Run unattended git network commands with
  `GCM_INTERACTIVE=never GIT_TERMINAL_PROMPT=0`.

Known follow-up: the deploy key logs in as `ubuntu`, which has sudo. Moving it to a dedicated
low-privilege deploy user would be safer.

## Local Clutter

These local files are untracked and not part of the site. Ignore them; don't commit or deploy them:
`welcome-vincent.html`, `assets/vincent-armenta.jpg`, `.codex-remote-attachments/`, `design-snapshots/`.

## Git Notes

Initial commit:

```text
c7cd0d2 Initial Datasail Solutions site
```

Logo update commit:

```text
dd2a7c4 Add DataSail logo treatment
```

When working from a new Codex project rooted here, verify:

```powershell
git status --short --branch
```

If Git complains about dubious ownership, this is because the repo was created by the user's Windows account and Codex may run as a sandbox user. The fix is to add the repo as a safe directory for the running user.

## User Preferences

- User is familiar with Claude Code and prefers low-friction execution.
- User dislikes frequent permission prompts.
- Best future workflow is to open a Codex project rooted directly at:

```text
C:\Codex Projects\DataSailSolutions\datasail-site
```

- Keep edits practical and visible.
- Commit and push when asked. Remember that pushing to `main` deploys to the live site.
