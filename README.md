# action-swiftlint

[![Test](https://github.com/nnsnodnb/action-swiftlint/workflows/Test/badge.svg)](https://github.com/nnsnodnb/action-swiftlint/actions?query=workflow%3ATest)
[![reviewdog](https://github.com/nnsnodnb/action-swiftlint/workflows/reviewdog/badge.svg)](https://github.com/nnsnodnb/action-swiftlint/actions?query=workflow%3Areviewdog)
[![depup](https://github.com/nnsnodnb/action-swiftlint/workflows/depup/badge.svg)](https://github.com/nnsnodnb/action-swiftlint/actions?query=workflow%3Adepup)
[![release](https://github.com/nnsnodnb/action-swiftlint/workflows/release/badge.svg)](https://github.com/nnsnodnb/action-swiftlint/actions?query=workflow%3Arelease)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/nnsnodnb/action-swiftlint?logo=github&sort=semver)](https://github.com/nnsnodnb/action-swiftlint/releases)
[![action-bumpr supported](https://img.shields.io/badge/bumpr-supported-ff69b4?logo=github&link=https://github.com/haya14busa/action-bumpr)](https://github.com/haya14busa/action-bumpr)

![github-pr-review demo](https://github.com/user-attachments/assets/7aae3127-f538-4654-9ef0-64950d25f90f)
![github-pr-check demo](https://github.com/user-attachments/assets/02dcb960-3d8e-4485-81ff-b3431d477287)

This action runs [SwiftLint](https://github.com/realm/SwiftLint) with [reviewdog](https://github.com/reviewdog/reviewdog) on pull requests to improve code review experience.

## Input

```yaml
inputs:
  github_token:
    description: 'GITHUB_TOKEN.'
    default: '${{ github.token }}'
    required: true
  tool_name:
    description: 'Tool name to use for reviewdog reporter'
    default: 'swiftlint'
    required: true
  level:
    description: 'Report level for reviewdog [info,warning,error]'
    default: 'error'
    required: true
  workdir:
    description: 'Working directory relative to the root directory.'
    default: '.'
  reporter:
    description: 'Reporter of reviewdog command [github-pr-check,github-check,github-pr-review].'
    default: 'github-pr-review'
  filter_mode:
    description: |
      Filtering mode for the reviewdog command [added,diff_context,file,nofilter].
      Default is added.
    default: 'added'
  fail_level:
    description: |
      If set to `none`, always use exit code 0 for reviewdog. Otherwise, exit code 1 for reviewdog if it finds at least 1 issue with severity greater than or equal to the given level.
      Possible values: [none,any,info,warning,error]
      Default is `none`.
    default: 'none'
  reviewdog_flags:
    description: 'Additional reviewdog flags'
    default: ''
  swiftlint_version:
    description: 'SwiftLint version to install'
    default: '0.63.2'
    required: true
```

## Usage

```yaml
name: reviewdog
on: [pull_request]
jobs:
  swiftlint:
    name: runner / swiftlint
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
      - uses: nnsnodnb/action-swiftlint@a353c9762a6c856eac886c6c4f0292e800d6dbb2 # v1.0.0
        with:
          github_token: ${{ secrets.github_token }}
          reporter: github-pr-review
          level: warning
```
