dockerhub-semantic-release-gh-action
===
[![LICENSE](https://img.shields.io/github/license/timo-reymann/dockerhub-semantic-release-gh-action)](https://github.com/timo-reymann/dockerhub-semantic-release-gh-action/blob/main/LICENSE)

<p align="center">
	<img width="300" src="https://avatars.githubusercontent.com/u/54465427?v=4">
    <br />
    Utilize semantic-release and publish images to docker hub automatically
</p>

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
    steps:
      - runs-on: ubuntu-latest
        uses: timo-reymann/dockerhub-semantic-release-gh-action@v6
        with:
          image: user/imagename
          dockerhub_username: ${{ secrets.DOCKERHUB_USERNAME }}
          dockerhub_token: ${{ secrets.DOCKERHUB_TOKEN }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

## Published tags

For a release `3.2.1` on `main` the action pushes these tags:

- `3`
- `3.2`
- `3.2.1`
- `latest`
- `edge`

The version tag keeps the full version text. A prerelease such as `3.2.1-beta.1` publishes `3`, `3.2`, `3.2.1-beta.1`, `latest` and `edge`.

| Run | Pushed tags |
| --- | --- |
| Release on `main` or `master` | `3`, `3.2`, `3.2.1`, `latest`, `edge` |
| Release on another branch | `3`, `3.2`, `3.2.1`, `latest` |
| No release on `main` or `master` | `edge` |
| No release on another branch | none (local `snapshot` build check only) |

