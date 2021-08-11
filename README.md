# cg-deploy-action

Github Action for deploying a cloud.gov application

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
        with:
          cf_username: ${{ secrets.CF_USERNAME }}
          cf_password: ${{ secrets.CF_PASSWORD }}
          cf_org: my-org-name
          cf_space: my-space-name
          push_arguments: "--vars-file deploy_config.yml --var OTHER_SECRET=${{ secrets.OTHER_SECRET }}"
```

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

## Outputs

None yet

## Testing locally

[Act](https://github.com/nektos/act) can be used to run the test workflow locally.

`act pull_request`
