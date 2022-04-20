# Tyk Github Actions Automation Example

This repository provides an example automation framework for publishing APIs on Tyk, utilising GitHub Actions.

In this example `tyk-sync` will synchronise a Tyk Dashboard with the contents of a Github repository. The sync is one way - from the repo to the Dashboard, the command will not write back to the repo. `tyk-sync` will delete any objects in the Dashboard that it cannot find in the github repo, and update those that it can find and create those that are missing.

# Steps

- use `tyk-sync` to export APIs from a source Tyk Dashboard, e.g. Development
- commit to git and push
- raise PR and merge to master
- the example GitHub Actions Workflow will syncronise the target Tyk Dashboard with the contents of the repo

## Prerequisites

- A git repository to store exported api definitions
- `tyk-sync` (https://tyk.io/docs/tyk-sync/) installed locally
- A Tyk installation from which you will export APIs
- A Tyk installation into which you will import APIs (configured in GitHub Actions workflow)


## Example Workflow

checkout new branch

```
git checkout -b sync-demo
```

export APIs from a source Tyk Dashboard, e.g. Development

```
tyk-sync dump -d="http://localhost:3000" -s="<dashboard-user-api-key>"
```

commit to git and push

```
git add . && git commit -m "sync demo" && git push
```

Open a pull request in github, then merge to master. This should trigger the GitHub Actions workflow to use `tyk-sync` to synchronise the target Tyk Dashboard with APIs in the master branch

