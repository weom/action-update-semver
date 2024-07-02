# GitHub Action: Update major/minor semver for GHE
This action updates major/minor release tags on a tag push.
e.g. Update `v1` and `v1.2` tag when released `v1.2.3`.

It works well for GitHub Action. ref: https://help.github.com/en/articles/about-actions#versioning-your-action

## Inputs

### `ghe_repo`

To specify your github enterprise url.

### `tag`

**Optional**. Existing tag to update from. Default comes from `$GITHUB_REF`.

### `message`

**Optional**. Tag message. Default: `Release $TAG`

### `major_version_tag_only`

**Optional**. Create only major version tags. Default: `false`

### `github_token`

**Optional**. It's no need to specify it if you use checkout@v2. Required for
checkout@v1 action.


## Example usage

### [.github/workflows/update_semver.yml](.github/workflows/update_semver.yml)

```yml
name: Update Semver
on:
  push:
    branches-ignore:
      - '**'
    tags:
      - 'v*.*.*'
jobs:
  update-semver:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: weom/action-update-semver@v1.0.4
        with:
          ghe_repo: <ghe url>
          major_version_tag_only: true  # (optional, default is "false")
```

<details>

<summary>oneliner</summary>

```
$ cat <<EOF > .github/workflows/update_semver.yml
name: Update Semver
on:
  push:
    branches-ignore:
      - '**'
    tags:
      - 'v*.*.*'
jobs:
  update-semver:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: weom/action-update-semver@v1.0.4
        with:
          github_token: \${{ secrets.github_token }}
EOF
```

</details>

### Acknowledgment
This action is based on [@haya14busa's update-major-minor-semver](https://github.com/haya14busa/action-update-semver).
