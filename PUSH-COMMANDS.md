# Push Commands — logan-portfolio

Run these from this directory (`Bob The Builder/logan-portfolio/`).

## 1. Create the GitHub repo (one time)

Replace `<PAT>` with your classic PAT (starts with `ghp_`):

```bash
curl -X POST -H "Authorization: token <PAT>" \
  -H "Accept: application/vnd.github+json" \
  https://api.github.com/user/repos \
  -d '{"name":"logan-portfolio","description":"Standalone interactive HTML builds","private":false,"has_issues":false,"has_projects":false,"has_wiki":false}'
```

## 2. Push the local commits

```bash
cd "/Users/loganmatson/Desktop/AI Work/Bob The Builder/logan-portfolio"
git remote add origin "https://loganmatson:<PAT>@github.com/loganmatson/logan-portfolio.git"
git push -u origin main
```

## 3. Enable GitHub Pages (one time)

```bash
curl -X POST -H "Authorization: token <PAT>" \
  -H "Accept: application/vnd.github+json" \
  https://api.github.com/repos/loganmatson/logan-portfolio/pages \
  -d '{"source":{"branch":"main","path":"/"}}'
```

After ~30 seconds, these will be live:

- https://loganmatson.github.io/logan-portfolio/
- https://loganmatson.github.io/logan-portfolio/marathon-plan.html
- https://loganmatson.github.io/logan-portfolio/scotland.html

## 4. Tell Logan / Claude to update the portfolio site

Two HTML comments in `Personal/Career/Personal Website/portfolio/index.html` mark the spots where the URLs need to swap from `#` to the live links:

```
<!-- TODO: replace href once Marathon Plan is pushed ... -->
<!-- TODO: replace href once Scotland Itinerary is pushed ... -->
```

Then remove the `data-pending` attribute from those two `<a>` tags.

## Security note

Once pushed, **revoke the PAT** at https://github.com/settings/tokens or rotate it. The token in the remote URL is stored in `.git/config` — either remove it (`git remote set-url origin https://github.com/loganmatson/logan-portfolio.git`) or use SSH for future pushes.
