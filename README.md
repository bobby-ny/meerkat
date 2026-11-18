<p align="center"><a href="https://meerkatsec.win/"><img src="meerkat.svg" alt="Meerkat" width="120" height="120"></a></p>

<h1 align="center">Meerkat</h1>

<p align="center"><b>Early warning system of vulnerabilities.</b><br>Know before the CVE.</p>

<p align="center"><a href="https://meerkatsec.win/">Website</a> · <a href="https://meerkatsec.win/waitlist">Join the waitlist</a> · <a href="https://meerkatsec.win/private-projects">Private projects</a> · <a href="https://meerkatsec.win/badge">Repo badge</a> · <a href="https://meerkatsec.win/pricing">Pricing</a></p>

Meerkat reads 1,000+ sources around the clock and emails you when a security problem touches the packages and products you run, often hours or days before a CVE exists.

## How it works

1. **Tell it what you run.** Point it at a GitHub repository, send a package list, or pick products by name.
2. **It keeps watch.** 1,000+ sources, around the clock, matched against the packages, versions and products you use.
3. **You hear first.** One email thread per issue, from first warning to fix to exploitation.

## Private code, in two steps

Your code stays with you. Meerkat receives package names and versions, and never needs access to your repository.

1. Create a private project at [meerkatsec.win](https://meerkatsec.win/app/projects) and set the upload key it gives you.
2. Run one command in your project folder.

With OSV-Scanner:

```bash
osv-scanner scan source -r --offline --download-offline-databases --all-packages --format cyclonedx-1-5 . \
  | jq '{bomFormat,components:[.components[]|select(.purl)|{purl}]}' \
  | curl --fail-with-body --silent --show-error --header "Authorization: Bearer $MEERKAT_UPLOAD_KEY" --header "Content-Type: application/json" --data-binary @- https://meerkatsec.win/api/v1/upload
```

Or with Syft:

```bash
SYFT_CHECK_FOR_APP_UPDATE=false syft . -o cyclonedx-json \
  | jq '{bomFormat,components:[.components[]|select(.purl)|{purl}]}' \
  | curl --fail-with-body --silent --show-error --header "Authorization: Bearer $MEERKAT_UPLOAD_KEY" --header "Content-Type: application/json" --data-binary @- https://meerkatsec.win/api/v1/upload
```

## Add the badge to your README

Replace `OWNER/REPO` with a public repository you maintain:

```markdown
[![Meerkat](https://meerkatsec.win/badge/github/OWNER/REPO.svg)](https://meerkatsec.win/r/github/OWNER/REPO)
```

## Plans

Meerkat is opening in weekly waves. [Join the waitlist](https://meerkatsec.win/waitlist). Paid plans skip it.

| | Individual | Team | Business |
| --- | --- | --- | --- |
| Price | Free | $5 per month | $50 per month |
| Projects | 3 | 15 | 100 |
| Extra watched items | 25 | 150 | 1,000 |
| Users | 1 | 5 | 25 |
| Private projects | 1 | 15 | 100 |
