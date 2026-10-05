# sync-my-repos

`sync-my-repos` interactively checks Git repositories directly inside `~/Developer` against their configured upstreams. It reports remote history separately from local working-tree changes and asks before fetching or pulling.

### Features

- Scans top-level directories in `~/Developer` and confirms each is a Git repository whose root is that directory.
- Shows the current branch, upstream, origin URL, and working-tree changes.
- Prompts with `Fetch and compare with remote? [y]es [N]o [a]ll [q]uit`.
- `a` approves fetch and comparison for the remaining repositories in that run only.
- Uses `git fetch --prune` to update remote-tracking information, then reports ahead and behind counts separately from working-tree cleanliness.
- Never pushes. A fast-forward pull is offered separately only when the remote is ahead and the working tree is clean; the pull prompt defaults to No.
- Does not automatically pull when the working tree is dirty, the local branch is ahead only, or the branches have diverged.
- `q` exits. Unrecognized or empty answers to the fetch prompt skip that repository.

## Requirements

- Bash
- Git
- Repositories under `~/Developer` with an upstream configured to compare against

## Installation

Copy the script to a directory on your `PATH` and make it executable. For this setup, the command can be installed with:

```sh
ln -s "$HOME/Developer/sync-my-repos/sync-my-repos" "$HOME/bin/sync-my-repos"
```

## Usage

```sh
sync-my-repos
```

## Behavior

The script fetches only after approval. It skips repositories without an active branch or configured upstream. A requested pull uses `git pull --ff-only`; a failed fetch or pull is reported and the scan continues where applicable.

## Limitations

Only immediate child directories of `~/Developer` are scanned. Nested repositories are not searched. Fetching contacts each configured remote and updates its remote-tracking information.
