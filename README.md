# Publish to GitHub PyPI

This action publishes a Python package to a GitHub-hosted PyPI repository. It extracts details from the `pyproject.toml` file and triggers a workflow in the PyPI repository to publish the package.

> **Note:** This is one of two actions that work together to publish a Python package to a GitHub-hosted PyPI repository. The other action is [the handler](https://github.com/bitovi/github-actions-publish-github-pypi-handler) that you need to add to the PyPI repository.

## Table of Contents
1. [Action Summary](#action-summary)
2. [Pre-requisites](#pre-requisites)
3. [Basic Use](#basic-use)
4. [Inputs](#inputs)
5. [Contributing](#contributing)
6. [License](#license)
7. [Provided by Bitovi](#provided-by-bitovi)
8. [We want to hear from you](#we-want-to-hear-from-you)

## Action Summary

This action publishes a Python package to a GitHub-hosted PyPI repository (a repository managed by the [handler action](https://github.com/bitovi/github-actions-publish-github-pypi-handler)):
1. Extract details from `pyproject.toml` file
2. Trigger a workflow in the PyPI repository

If you would like to deploy other types of applications, check out our other actions:
| Action | Purpose |
| ------ | ------- |
| [Deploy Docker to EC2](https://github.com/marketplace/actions/deploy-docker-to-aws-ec2) | Deploys a repo with a Dockerized application to a virtual machine (EC2) on AWS |
| [Deploy Storybook to GitHub Pages](https://github.com/marketplace/actions/deploy-storybook-to-github-pages) | Builds and deploys a Storybook application to GitHub Pages. |
| [Deploy static site to AWS (S3/CDN/R53)](https://github.com/marketplace/actions/deploy-static-site-to-aws-s3-cdn-r53) | Hosts a static site in AWS S3 with CloudFront |
<br/>

**And more!**, check our [list of actions in the GitHub marketplace](https://github.com/marketplace?category=&type=actions&verification=&query=bitovi)

## Need help or have questions?

This project is supported by [Bitovi, A DevOps consultancy](https://www.bitovi.com/services/devops-consulting).

You can **get help or ask questions** on our:

- [Discord Community](https://discord.gg/zAHn4JBVcX)

Or, you can hire us for training, consulting, or development. [Set up a free consultation](https://www.bitovi.com/services/devops-consulting).

## Pre-requisites
- A GitHub-hosted PyPI repository with a workflow that uses the corresponding handler action (e.g. `publish-handler.yaml`). To set this up, follow the instructions in the [handler action](https://github.com/bitovi/github-actions-publish-github-pypi-handler)
- A GitHub repository with a Python package
- A `pyproject.toml` file in the root of the repository
- A GitHub token with `repo` scope added to the repository secrets


## Basic Use

For basic usage, create `.github/workflows/publish.yaml` with the following to build and publish on push to a tag:

```yaml
on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Publish to PyPI
        uses: bitovi/github-actions-publish-github-pypi@v0.1.0
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          pypi-github-org: 'your-github-org'
          pypi-github-repo: 'your-pypi-repo'
          pypi-github-workflow-filename: 'publish-handler.yaml'
```

## Inputs

The following inputs can be used as `step.with` keys:

| Name                               | Type    | Description                                                                            |
|------------------------------------|---------|----------------------------------------------------------------------------------------|
| `pypi-github-org`                  | String  | (Required) The GitHub organization of the PyPI repository                               |
| `pypi-github-repo`                 | String  | (Required) The GitHub repository for the PyPI package                                   |
| `github-token`                     | String  | (Required) The GitHub token to use for triggering the publish workflow in the PyPI repository |
| `pypi-github-user`                 | String  | (Optional) The GitHub user to publish the package. Default is `pypi-publisher[bot]`     |
| `pypi-github-workflow-filename`    | String  | (Optional) The GitHub workflow filename to trigger. Default is `publish-trigger.yaml`   |
| `pypi-github-workflow-ref`         | String  | (Optional) The GitHub branch or ref to use when triggering the workflow. Default is `main` |
| `checkout`                         | Boolean | (Optional) Whether to checkout the repository. Default is `true`                        |
| `python-version`                   | String  | (Required) The Python version to use. Default is `3.8`                                  |
| `toml-file`                        | String  | (Optional) Path to the `pyproject.toml` file. Default is `pyproject.toml`               |

## Contributing

We would love for you to contribute to this action. [Issues](https://github.com/bitovi/github-actions-publish-github-pypi/issues/new/choose) and Pull Requests are welcome!

## License

The scripts and documentation in this project are released under the MIT License.

# Provided by Bitovi

[Bitovi](https://www.bitovi.com/) is a proud supporter of Open Source software.

# We want to hear from you.

Come chat with us about open source in our Bitovi community [Discord](https://discord.gg/J7ejFsZnJ4Z)!
```