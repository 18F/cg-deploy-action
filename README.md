# cg-deploy-action

Github Action for deploying a cloud.gov application

DEPRECATED: This action has been deprecated in favor of [an alternative GitHub Action supported by the cloud.gov team](https://github.com/cloud-gov/cg-cli-tools).

## Example use

```
name: CD
on: [push]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Deploy to cloud.gov
        uses: 18f/cg-deploy-action@main
        env:
          OTHER_SECRET: ${{ secrets.OTHER_SECRET }}
        with:
          cf_username: ${{ secrets.CF_USERNAME }}
          cf_password: ${{ secrets.CF_PASSWORD }}
          cf_org: my-org-name
          cf_space: my-space-name
          push_arguments: >-
            --vars-file deploy_config.yml
            --var other_secret="$OTHER_SECRET"

      - name: Set environment variable
        uses: 18f/cg-deploy-action@main
        with:
          cf_username: ${{ secrets.CF_USERNAME }}
          cf_password: ${{ secrets.CF_PASSWORD }}
          cf_org: my-org-name
          cf_space: my-space-name
          full_command: "cf set-env APP_NAME DEPLOYED_SHA $GITHUB_SHA"
```

### Important Gotcha

To use multiline strings for `push_arguments` or `full_command` use the `>-` form that tells yaml to strip out newlines

## Inputs

| Name | Description | Required | Default |
| ---- | ----------- | -------- | ------- |
| `cf_username` | Deploy user cloud.gov username | Yes | |
| `cf_password` | Deploy user cloud.gov password | Yes | |
| `cf_org` | cloud.gov organization to deploy to | Yes | |
| `cf_space` | cloud.gov space to deploy to | Yes | |
| `push_arguments` | Additional arguments to pass to cf push | No | |
| `cf_api` | API endpoint for cloudfoundry server | No | `https://api.fr.cloud.gov` |
| `app_directory` | Directory to push to cloud.gov | No | `./` |
| `full_command` | Full command to run instead of `cf push` | No | |

## Outputs

None yet

## Testing locally

[Act](https://github.com/nektos/act) can be used to run the test workflow locally.

1. `$ cp .secrets.example .secrets`
1. Create a [space-deployer service account](https://cloud.gov/docs/services/cloud-gov-service-account/) and copy the username and password into `.secrets`
1. Set `CF_ORG` and `CF_SPACE` to your organization and space
1. Run act: `$ act`
