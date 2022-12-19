# github-actions

Set of GitHub actions to be used among applications and libraries.

## Deploy application

This GitHub action contains all the necesary steps to create a release and deploy an application into the Google firebase.

### Example

```yml
name: Continuous Integration & Deployment
permissions: write-all
on:
  push:
    tags:
      - v*

jobs:
  deploy-app:
    name: Deploy application
    runs-on: ubuntu-latest
    concurrency:
      group: ${{ github.workflow }}-deploy-app
      cancel-in-progress: true

    steps:
      - uses: agusmgarcia/github-actions/deploy-app@<PACKAGE-VERSION>
        with:
          firebase-token: ${{ secrets.FIREBASE_TOKEN }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

> Replace `<PACKAGE-VERSION>` by the existing version you want to use.

## Publish library

This GitHub action contains all the necesary steps to create a release and publish an NPM library into the GitHub registry.

### Example

```yml
name: Continuous Integration & Deployment
permissions: write-all
on:
  push:
    tags:
      - v*

jobs:
  publish-lib:
    name: Publish library
    runs-on: ubuntu-latest
    concurrency:
      group: ${{ github.workflow }}-publish-lib
      cancel-in-progress: true

    steps:
      - uses: agusmgarcia/github-actions/publish-lib@<PACKAGE-VERSION>
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

> Replace `<PACKAGE-VERSION>` by the existing version you want to use.
