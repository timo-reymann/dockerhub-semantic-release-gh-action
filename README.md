dockerhub-semantic-release-gh-action
===

Utilize semantic-release and publish images to docker hub automatically


## Required for usage

- docker hub account
- Dockerfile is present in root folder
- Token for pushing and updating the repo on docker hub


## Usage

```yaml
name: Continuous build and release docker image
on:
  push:
    branches:
      - master
      - main
permissions:
  contents: write
jobs:
  main:
    runs-on: ubuntu-latest
    uses: timo-reymann/docker-semantic-release-gh-action@v1
    with:
      image: user/imagename
```
