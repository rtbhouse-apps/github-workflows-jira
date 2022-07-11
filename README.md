# github-workflows-jira
This workflow automatically adds to pull request comment with link to Jira item. Jira ID (like `APPS-XXXXX`)
must be somwhere in the pull request's title.

If PR title doesn't contain valid Jira ID following comment will be added:
> PR title should contain Jira ID like `JIRA-1234`


## Setup
Update `jira-instance-url` and `jira-project-id` in `add_jira_link_to_pr.yaml` file in this repo accordingly.
You may also set up them directly when referencing this workflow (please see next section).   

## Using workflow in own repo
Create YAML file in `.github/workflows` in your repository

#### Sample content of file:
```
name: "Add link to Jira item in PR"

on:
  pull_request:
    types:
      - opened
      - edited

jobs:
  jira_pr_comment:
    name: "Add comment to PR"
    uses: "rtbhouse-apps/github-workflows-jira/.github/workflows/add_jira_link_to_pr.yaml@v0"
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN }}
```

You may also override parameters `jira-instance-url` and `jira-project-id` in `with` section:
```
jobs:
  jira_pr_comment:
    name: "Add comment to PR"
    uses: "rtbhouse-apps/github-workflows-jira/.github/workflows/add_jira_link_to_pr.yaml@v0"
    with:
      jira-instance-url: "https://my_jira_instance.atlassian.net/browse"
      jira-project-id: "MYJIRAPROJECT"
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN }}
```
