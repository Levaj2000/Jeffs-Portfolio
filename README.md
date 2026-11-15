# Jeff Leva portfolio (static site for Vercel)

```
site/
├── vercel.json        # serves public/, clean URLs, security headers (CSP, HSTS, ...)
└── public/
    ├── index.html     # the page
    ├── styles.css     # all styles (no inline CSS, so the CSP needs no 'unsafe-inline')
    ├── favicon.svg
    ├── og.png         # 1200x630 link-preview image
    └── fonts/         # self-hosted IBM Plex (SIL OFL 1.1, license included)
```

No build step. Open public/index.html locally to preview.

## Before the first deploy
- The canonical, og:url, og:image and JSON-LD url use `https://jeff-leva.vercel.app/`.
  If Vercel gives the project a different URL, or you add a custom domain, replace it:
  `grep -rl jeff-leva.vercel.app public | xargs sed -i 's#https://jeff-leva.vercel.app#https://YOUR-DOMAIN#g'`
- Optional: add a general-purpose `resume.pdf` to public/ and uncomment the Résumé button in index.html.

## Deploy (Git integration, recommended)
1. Create a repo (e.g. `Levaj2000/portfolio`, private is fine) and push the contents of `site/` to it.
2. vercel.com > Add New > Project > import the repo. Framework preset: Other. Leave build settings empty
   (vercel.json sets the output directory to `public`). Project name `jeff-leva`.
3. Deploy. Every push to main redeploys; branches get preview URLs.

## Deploy (CLI, no repo)
```
npm i -g vercel
cd site
vercel          # first run links/creates the project; answer "jeff-leva" for the name
vercel --prod
```

## Custom domain (optional, ~$10-15/yr for a .com)
Project > Settings > Domains > add the domain. Buy it through Vercel, or at any registrar and point
the apex A record to 76.76.21.21 and `www` CNAME to cname.vercel-dns.com (Vercel shows the exact
records). HTTPS is automatic. Then update the URLs above and redeploy.

## After it's live
- Check headers: `curl -sI https://YOUR-URL | grep -iE 'content-security|strict-transport'`
- Test the link preview with LinkedIn's Post Inspector.
- Add the URL to LinkedIn (Featured + Contact info), the GitHub profile README, and résumé headers.
