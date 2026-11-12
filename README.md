# IWC Lab

Sandbox mirror of the [IWC](https://github.com/galaxyproject/iwc) deploy pipeline for
experimental and Format-2 workflows.

Workflows merged here are deployed to the
[iwc-lab-workflows](https://github.com/iwc-lab-workflows) GitHub organization and
registered on Dockstore (`organization:iwc-lab-workflows`). Nothing here is installed
on usegalaxy.\* servers, and nothing is registered on WorkflowHub.

The pipeline is live. `workflows/epigenetics/average-bigwig-between-replicates` is a
copy of an IWC workflow kept here to prove it out end to end: it is deployed, released
independently as v0.2, and tested nightly. Treat it as scaffolding rather than as
content -- real Format-2 workflows are the point of this repository.

## Website

The workflows here are browsable at [iwc-lab.galaxyproject.org](https://iwc-lab.galaxyproject.org).
The site is IWC's: `.github/workflows/gh-page-build.yml` checks out
[galaxyproject/iwc](https://github.com/galaxyproject/iwc) at the commit in `website/iwc-ref`,
runs its manifest script over this repository's `workflows/`, and builds its Astro site with
`website/site-config.json` in place of IWC's own values. Nothing of the site's code lives here.
See "Building a second site" in IWC's
[website README](https://github.com/galaxyproject/iwc/blob/main/website/README.md) for what
each config key does.

- `website/site-config.json` -- the lab's name, wording, links and Dockstore organization.
- `website/about.md` -- the about page.
- `website/iwc-ref` -- the IWC commit the site is built from. It has to be a full SHA on IWC's
  `main`.

The site is rebuilt on every push to `main` and once a day. A workflow appears once Dockstore
has registered it under `iwc-lab-workflows`, which is some time after the merge that deployed
it, so a new workflow can take until the next daily build to show up.

### Moving to a newer IWC commit

Changes to IWC's site reach this one only when `website/iwc-ref` is changed. Open a pull
request that replaces the SHA with a newer one from IWC's `main`. The pull request builds the
site without deploying it, and the result is attached to the run as the `site` artifact. If IWC
has added a config key since the last pin, the build fails and names the key; add it to
`website/site-config.json` in the same pull request.
