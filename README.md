# FLECS Create GitHub Secret Action
A GitHub action to create or update GitHub repository and organization secrets

# Usage
## Examples for repository secrets
### Create or update secret in current repository
```yml
uses: FLECS-Technologies/create-github-secret-action@v1.x
with:
  name: "MY_SECRET"
  value: "my_secret_value"
env:
  GITHUB_TOKEN: "access token with with secrets repo permission"
```

### Create or update secret in other repository
```yml
uses: FLECS-Technologies/create-github-secret-action@v1.x
with:
  repo: "repository-name"
  owner: "organization"
  name: "MY_SECRET"
  value: "my_secret_value"
env:
  GITHUB_TOKEN: "access token with with secrets repo permission"
```
## Example for organization secret
```yml
uses: FLECS-Technologies/create-github-secret-action@v1.x
with:
  org: "some-org"
  visibility: "select"
  repos: "awesome-project-1, awesome-project-2"
  name: "MY_SECRET"
  value: "my_secret_value"
env:
  GITHUB_TOKEN: "access token with with secrets organization permission"
```

# Inputs
## Common
| Name          | Description             | Example           | Required | Default |
| ------------- | ----------------------- | ----------------- | -------- | ------- |
| name          | Name of the secret      | "MY_SECRET"       | Yes      | -       |
| value         | Value of the secret     | "my_secret_value" | Yes      | -       |

## Repository secrets (default)
| Name          | Description             | Example              | Required        | Default                          |
| ------------- | ----------------------- | -------------------- | --------------- | -------------------------------- |
| repo          | Name of the repository  | "awesome-project"    | Yes, if `owner` | `${{ github.repository_name }}`* |
| owner         | Repository owner        | "FLECS-Technologies" | No              | `${{ github.repository_owner }}` |

\* "Name" part of `${{ github.repository }}`, i.e. "owner/repository-name" -> "repository-name"

## Organization secrets
| Name          | Description                                                        | Example               | Required         | Default   |
| ------------- | ------------------------------------------------------------------ | --------------------- | ---------------- | --------- |
| org           | Name of the organization                                           | "FLECS-Technologies"  | Yes              | -         |
| visibility    | Secret visibility (one of "private"\|"all"\|"select")              | "private"             | No               | "private" |
| repos         | Comma-separated list of repository names with access to the secret | "repo1, repo2, repo3" | Yes, if "select" | -         |

See [GitHub REST API documentation for organization secrets]([https://docs.github.com/en/rest/actions/secrets?apiVersion=2022-11-28#create-or-update-an-organization-secret) or [GitHub REST API documentation for repository secrets](https://docs.github.com/en/rest/actions/secrets?apiVersion=2022-11-28#create-or-update-a-repository-secret) for further examples and explanation.

# Environment
## Repository secrets
| Name          | Description                                                                                                  | Required |
| ------------- | ------------------------------------------------------------------------------------------------------------ | ---------|
| GITHUB\_TOKEN | A GitHub access token or GitHub Apps installastion token with the "Secrets" repository permissions (write)   | true     |

## Organization secrets
| Name          | Description                                                                                                  | Required |
| ------------- | ------------------------------------------------------------------------------------------------------------ | ---------|
| GITHUB\_TOKEN | A GitHub access token or GitHub Apps installastion token with the "Secrets" organization permissions (write) | true     |

# License
[Apache 2.0](https://github.com/FLECS-Technologies/create-github-secret-action/blob/v1.x/LICENSE)
