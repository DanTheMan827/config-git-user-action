# Configure Git for GitHub User

This GitHub Action configures git with the GitHub user information.

## Inputs

| Name                | Description                                                                                                            | Required | Default |
|---------------------|------------------------------------------------------------------------------------------------------------------------|----------|---------|
| `user_name`         | The GitHub username. If not provided, the current workflow actor will be used.                                         | false    |         |
| `git_name`          | The override name to use for git.                                                                                      | false    |         |
| `use_real_name`     | Prefer real name if available instead of the GitHub username. This has no effect if `git_name` is provided.            | false    | true    |
| `prefer_user_email` | Prefer user email if available instead of noreply GitHub email.                                                        | false    | false   |
| `token`             | The GitHub token to use for API requests. If not provided the action will be subject to unauthenticated rate limits.   | false    |         |

## Outputs

| Name    | Description                |
|---------|----------------------------|
| `name`  | The configured git name    |
| `email` | The configured git email   |

## Example Usage

```yaml
name: Configure Git Example

jobs:
  configure-git:
    runs-on: ubuntu-latest
    steps:
      - name: Configure Git
        uses: DanTheMan827/config-git-user-action@main
        with:
            user_name: 'octocat'
            use_real_name: true
            token: ${{ secrets.GITHUB_TOKEN }}
```

## How It Works

1. **Get user info**: Retrieves user information from the GitHub API.
2. **Configure git name**: Sets the git user name.
3. **Configure git email**: Sets the git user email.

This action uses a composite run step to execute the necessary commands to configure git with the provided or derived user information.