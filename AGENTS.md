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

## Existing Infrastructure Context

Related SentrySail docs found at:

```text
C:\Users\mikel\code\sentrysail\INTEGRATIONS.md
```

Relevant existing infrastructure:

- AWS Lightsail server
- Ubuntu
- Nginx
- PM2 for SentrySail Next.js app
- Existing server IP from SentrySail notes: `54.191.209.220`
- SSH shortcut from SentrySail notes: `ssh sentrysail`
- Cloudflare used for DNS/security/email routing for SentrySail
- GoDaddy used as registrar
- Existing deploy style for SentrySail: `git pull`, `npm run build`, `pm2 restart sentrysail`

For this DataSail site:

- Static HTML/CSS/JS means PM2 is not needed.
- Nginx can serve the files directly.
- Good deployment path: GitHub repo -> git pull on Lightsail -> Nginx static server block for `datasailsolutions.com` / `www.datasailsolutions.com`.

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
- Commit and push when asked.
