# info-workflows

Public GitHub Actions for the Info Agent's ".info" sites
([info-sites-org/info-agent](https://github.com/info-sites-org/info-agent), private).
Public so the builds run on free GitHub runners; the agent and site repos stay
private, and keys live only in this repo's encrypted secrets.

- [Deploy](.github/workflows/deploy.yml): builds a site with the agent's shared
  theme and the Hugo version in its profile, and uploads it to the site's Ceph
  bucket (`qa-<site>` or `www-<site>`). The agent creates the bucket and starts
  the run.
- [Autopilot](.github/workflows/autopilot.yml): every day drafts each site's
  new pages from checked facts and saves them on the agent blog for review,
  and on Mondays saves the week's report there (info-agent I-040). It commits
  the drafts to the agent repo and publishes nothing. It turns its own schedule
  back on each run, since GitHub turns off a public repo's schedules after 60
  quiet days.

Secrets: `INFO_REPOS_PAT`, `CEPH_REGION`, and for each environment
`CEPH_QA_*` / `CEPH_PRODUCTION_*` (`ACCESS_KEY_ID`, `SECRET_ACCESS_KEY`,
`ENDPOINT`). Production keys are added at go-live. Autopilot adds
`PROFESSIONALIZE_BASE_URL`, `PROFESSIONALIZE_API_SERVICE_KEY`,
`TAVILY_API_KEY`, `WORDPRESS_API_*` and `GOOGLE_KEY`. `python -m info_agent
secrets` sets them all from the agent's keys.
