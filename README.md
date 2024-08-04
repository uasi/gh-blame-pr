# `gh-blame-pr`

A [GitHub CLI](https://github.com/cli/cli) extension to open the most recent pull request that modified the specified file.

`gh-blame-pr` uses `git blame` under the hood and extract the pull request numbers included in the commit messages.

## Dependencies

- Ruby \>= 2.7
- [`git when-merged`](https://github.com/mhagger/git-when-merged)

## Installation

```
gh extension install uasi/gh-blame-pr
```

## Usage

```
gh blame-pr [<options>] [--] <path>
```

## Options

- `--ignore-squash`: Disable heuristics for detecting squash merge
- `-L <range>`: Blame only the line range (can be specified multiple times; see [`git help blame`](https://git-scm.com/docs/git-blame#Documentation/git-blame.txt--Lltstartgtltendgt) for details)
- `-l`, `--log`: Print the log of the merge commit and the commit that actually modified the file
- `-n <number>`, `--max-count=<number>`: Open the `<number>` most recent pull requests (defaults to 1)
- `-m <branch>`, `--merged-to=<branch>`: The branch name into which the pull request might have merged to (defaults to HEAD; can be specified multiple times)
- `-p`, `--print`, `--no-browser`: Print pull request URL instead of opening the browser

## Examples

```
% git clone --branch=v2.54.0 https://github.com/cli/cli.git
% cd cli

% gh blame-pr cmd/gh/main.go
Opening github.com/cli/cli/issues/8449 in your browser.

% gh blame-pr --max-count=2 --no-browser --log cmd/gh/main.go
https://github.com/cli/cli/issues/8449

commit 0f39935cc17c687232776ad4a4db2172559f2a86
(snip)

    Merge pull request #8449 from cli/wm/remove-redundant-err
    
    Remove redundant error on migration failure

commit cceec8e0d015648c3930f309759216ea5351e1d1
(snip)

    Remove redundant error on migration failure

https://github.com/cli/cli/issues/8425

commit 54d56cab3a0882b43ac794df59924dc3f93bb75c
(snip)

    Merge pull request #8425 from cli/wm/multi-account-ux-rebase
    
    Support multiple accounts on a single host

commit eb771aecc9eaf88e0dfdc302b516a7801714f6f8
(snip)

    Address PR comments
```
