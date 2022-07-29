# Publish AUR package

GitHub Actions to publish AUR package.

## Inputs

### `pkgname`

**Required** AUR package name.

### `pkgbuild`

**Required** Path to PKGBUILD file. This file is often generated by prior steps.

### `assets`

**Optional** Newline-separated glob patterns for additional files to be added to the AUR repository.
Glob patterns will be expanded by bash when copying the files to the repository.

### `updpkgsums`

**Optional** Update checksums using `updpkgsums`.

### `commit_username`

**Required** The username to use when creating the new commit.

### `commit_email`

**Required** The email to use when creating the new commit.

### `ssh_private_key`

**Required** Your private key with access to AUR package.

### `commit_message`

**Optional** Commit message to use when creating the new commit.

### `allow_empty_commits`

**Optional** Allow empty commits, i.e. commits with no change. The default value is `true`.

### `force_push`

**Optional** Use `--force` when push to the AUR. The default value is `false`.

### `ssh_keyscan_types`

**Optional** Comma-separated list of types to use when adding aur.archlinux.org to known hosts.

## Example usage

```yaml
name: aur-publish

on:
  push:
    tags:
      - '*'

jobs:
  aur-publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Publish AUR package
        uses: KSXGitHub/github-actions-deploy-aur@<TAG>
        with:
          pkgname: my-awesome-package
          pkgbuild: ./PKGBUILD
          commit_username: ${{ secrets.AUR_USERNAME }}
          commit_email: ${{ secrets.AUR_EMAIL }}
          ssh_private_key: ${{ secrets.AUR_SSH_PRIVATE_KEY }}
          commit_message: Update AUR package
          ssh_keyscan_types: rsa,dsa,ecdsa,ed25519
```

**Note:** Replace `<TAG>` in the above code snippet with a tag of this repo.

**Tip:** To create secrets (such as `secrets.AUR_USERNAME`, `secrets.AUR_EMAIL`, and `secrets.AUR_SSH_PRIVATE_KEY` above), go to `$YOUR_GITHUB_REPO_URL/settings/secrets`. [Read this for more information](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets).

**Tip:** This action does not generate PKGBUILD for you, you must generate it yourself (e.g. by using actions before this action).

## Real-world applications

[sane-fmt](https://github.com/KSXGitHub/sane-fmt) has a [workflow](https://github.com/KSXGitHub/sane-fmt/blob/c07ce4f09c0b8dfa902d28753ebb3800268183f5/.github/workflows/deploy.yaml) that builds and uploads executables to GitHub Release then generates PKGBUILD files for and use this very action to update [aur/sane-fmt](https://aur.archlinux.org/packages/sane-fmt) and [aur/sane-fmt-bin](https://aur.archlinux.org/packages/sane-fmt-bin).

[pretty-exec](https://github.com/KSXGitHub/pretty-exec) has a [workflow](https://github.com/KSXGitHub/pretty-exec/blob/67473cd85f6aa278367e30fce9e41b4e54e4cb82/.github/workflows/deploy.yaml) that builds and uploads executables to GitHub Release then generates PKGBUILD files for and use this very action to update [aur/pretty-exec](https://aur.archlinux.org/packages/pretty-exec/) and [aur/pretty-exec-bin](https://aur.archlinux.org/packages/pretty-exec-bin/).

[build-fs-tree](https://github.com/KSXGitHub/build-fs-tree) has a [workflow](https://github.com/KSXGitHub/build-fs-tree/blob/24924d99ae5cd82f00ea62fe8abc1a187bea7a0b/.github/workflows/deploy.yaml) that builds and uploads executables to GitHub Release then generates PKGBUILD files for and use this very action to update [aur/build-fs-tree](https://aur.archlinux.org/packages/build-fs-tree/) and [aur/build-fs-tree-bin](https://aur.archlinux.org/packages/build-fs-tree-bin/).

[strip-ansi-cli](https://github.com/KSXGitHub/strip-ansi-cli) has a [workflow](https://github.com/KSXGitHub/strip-ansi-cli/blob/f3de1cf4997bbc2efbf137f77325f12640c2e145/.github/workflows/deploy.yaml) that builds and uploads executables to GitHub Release then generates PKGBUILD files for and use this very action to update [aur/strip-ansi](https://aur.archlinux.org/packages/strip-ansi/) and [aur/strip-ansi-bin](https://aur.archlinux.org/packages/strip-ansi-bin/).

[parallel-disk-usage](https://github.com/KSXGitHub/parallel-disk-usage) has a [workflow](https://github.com/KSXGitHub/parallel-disk-usage/blob/a7fc0937a64d23ae848e44f7ecbf02aec64831e4/.github/workflows/deploy.yaml) that builds and uploads executables to GitHub Release then generates PKGBUILD files for and use this very action to update [aur/parallel-disk-usage](https://aur.archlinux.org/packages/parallel-disk-usage/) and [aur/parallel-disk-usage-bin](https://aur.archlinux.org/packages/parallel-disk-usage-bin/).

## Become a Patron

[My Patreon Page](https://patreon.com/khai96_).

## License

[MIT](https://git.io/JfWEM) © [Hoàng Văn Khải](https://github.com/KSXGitHub/)
