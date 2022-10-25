# Connect Artifactory Push Action

[![Tests](https://github.com/aisightgmbh/actions-connect-artifactory-push/actions/workflows/on_push.yaml/badge.svg)](https://github.com/aisightgmbh/actions-connect-artifactory-push/actions/workflows/on_push.yaml)

This action can be used to create credentials to push to AWS CodeArtifact.
The credentials are generated with the AWS CLI and put into the environment variables `POETRY_HTTP_BASIC_ARTIFACTORY_USERNAME` and `POETRY_HTTP_BASIC_ARTIFACTORY_PASSWORD`.
The url to publish to is stored in `POETRY_REPOSITORIES_PUBLISH_URL`.
This makes the artifactory available for Poetry under the name `publish`.
By default, the action will install the AWS CLI on the runner.
This behavior can be disabled by setting `install-aws`.

## Example

```yaml
jobs:
  example-job:
    runs-on: <YourCustomRunner>
    steps:
      - uses: actions/checkout@v3
      - uses: aisightgmbh/actions-connect-artifactory-push@v1
        with:
          artifactory-owner: ${{ secrets.owner }}
          artifactory-domain: ${{ secrets.domain }}
          artifactory-name: ${{ secrets.name }}
          install-aws: true
      - uses: aisightgmbh/actions-install-poetry@v1
      - run: poetry publish -r publish
```
