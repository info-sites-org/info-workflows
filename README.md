# info-workflows

Public GitHub Actions for the Info Agent's ".info" sites
([info-sites-org/info-agent](https://github.com/info-sites-org/info-agent), private).
Public so the builds run on free GitHub runners; the agent and site repos stay
private, and keys live only in this repo's encrypted secrets.

- [Deploy](.github/workflows/deploy.yml): builds a site with the agent's shared
  theme and the Hugo version in its profile, and uploads it to the site's Ceph
  bucket (`qa-<site>` or `www-<site>`). The agent creates the bucket and starts
  the run.

Secrets: `INFO_REPOS_PAT`, `CEPH_REGION`, and for each environment
`CEPH_QA_*` / `CEPH_PRODUCTION_*` (`ACCESS_KEY_ID`, `SECRET_ACCESS_KEY`,
`ENDPOINT`). Production keys are added at go-live.
