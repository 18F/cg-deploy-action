# cg-deploy-action

Github Action for deploying a cloud.gov application

## Example use


## Inputs

| Name | Description | Required | Default |
| ---- | ----------- | -------- | ------- |
| `cf_username` | Deploy user cloud.gov username | Yes | |
| `cf_password` | Deploy user cloud.gov password | Yes | |
| `cf_org` | cloud.gov organization to deploy to | Yes | |
| `cf_space` | cloud.gov space to deploy to | Yes | |
| `cf_api` | API endpoint for cloudfoundry server | No | `https://api.fr.cloud.gov` |
| `app_directory` | Directory to push to cloud.gov | No | `./` |

## Outputs

None yet
