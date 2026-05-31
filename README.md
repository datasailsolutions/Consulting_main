# Datasail Solutions Website

Static website draft for Datasail Solutions.

## Local Preview

From this folder:

```powershell
node dev-server.js
```

Then open:

```text
http://127.0.0.1:4173/
```

## Files

- `index.html` - Homepage
- `services.html` - Services overview
- `about.html` - Company positioning and point of view
- `contact.html` - Contact page
- `css/styles.css` - Shared site styling
- `js/main.js` - Mobile navigation behavior
- `assets/hero-pattern.svg` - Homepage hero visual

## Deployment Shape

This is a plain static site. For Lightsail, the deployable files are the HTML pages plus the `css`, `js`, and `assets` folders. They can be served directly by Nginx or Apache without a build step.
