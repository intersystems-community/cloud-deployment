InterSystems Dev Cloud Deployment
===

Usage
==

In your repository create file `.github/workflows/deploy.yml` with content. Replace `<deployment-name>` with the domain name, which will be used before `.sandbox.developer.intersystems.com`. Ask for deployment key and set it to secrets as `SERVICE_ACCOUNT_KEY`

```yaml
name: Dev Cloud Deploy

on:
  push:
    branches:
    - master
    - main
  workflow_dispatch:

jobs:
  deploy:
    uses: intersystems-community/cloud-deployment/.github/workflows/deployment.yml@main
    with:
      name: <deployment-name>
      ## Optional
      # memory: 1Gi
      # port: 8081
    secrets:
      SERVICE_ACCOUNT_KEY: ${{ secrets.SERVICE_ACCOUNT_KEY }}
      ## Optional
      # CUSTOM_VARS_LIST: "var1=${{ secrets.CUSTOM_VAR1 }},var2=value2,..."
```

Stopped deployments
==

A deployment stopped in the Developer Cloud UI stays stopped: the workflow checks the instance first and skips the build and deploy when it is stopped. Start it in the UI, then push again (or re-run the workflow) to deploy the latest commit.
