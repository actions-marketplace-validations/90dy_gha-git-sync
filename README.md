# Git Sync Github Action

![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/90dy/gha-git-sync/semantic-release.yml)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/90dy/gha-git-sync)

This GitHub Action enables you to synchronize the latest changes from another repository, streamlining your development process.

## Usage

To use this GitHub Action, add the following YAML code to your workflow file (e.g., `.github/workflows/git-sync.yml`):

```yaml
name: Git Sync

on:
  push:
    branches:
      - main

jobs:
  sync:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
        with:
          branch: main # Branch to sync in

      - name: Git Sync
        uses: 90dy/gha-git-sync@v1
        with:
          repository: '' # Repository to pull from
          branch: '' # Branch to sync from
          user-email: '' # Git user email
          user-name: '' # Git user name
          paths: | # File path to sync (not directories)
            file-a.txt
            file-b.txt
          commit-message: '' # Commit message
          assignees: '' # A comma or newline-separated list of assignees (GitHub usernames)
```

You can configure the following inputs based on your requirements:

- `repository`: The repository to pull changes from.
- `branch`: The branch to sync.
- `user-email`: Your Git user email.
- `user-name`: Your Git user name.
- `paths`: (Optional) File path to sync (not directories).
- `commit-message`: (Optional) Commit message.
- `assignees`: (Optional) A comma or newline-separated list of assignees (GitHub usernames).

## Workflow

1. Set the committer information in the Git configuration.
2. Fetch the changes from the specified repository and branch.
3. Checkout a new branch named after the repository and branch you are syncing from.
4. Attempt to rebase the changes and push them to the current branch.
5. If the rebase is successful, merge the changes into the current branch.
6. If the merge is successful, push the changes to the current branch.
7. If the rebase fails, abort the process.
8. If the abort is successful, create a pull request to sync the changes.

## License

This GitHub Action is licensed under the Unlicense License. See the [LICENSE](LICENSE) file for details.
