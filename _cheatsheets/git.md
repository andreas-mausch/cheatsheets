---
layout: cheatsheet
tags: vcs bundle
logo: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4NCjwhLS0gR2VuZXJhdG9yOiBBZG9iZSBJbGx1c3RyYXRvciAxNi4wLjAsIFNWRyBFeHBvcnQgUGx1Zy1JbiAuIFNWRyBWZXJzaW9uOiA2LjAwIEJ1aWxkIDApICAtLT4NCjwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+DQo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4Ig0KCSB3aWR0aD0iOTdweCIgaGVpZ2h0PSI5N3B4IiB2aWV3Qm94PSIwIDAgOTcgOTciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDk3IDk3IiB4bWw6c3BhY2U9InByZXNlcnZlIj4NCjxnPg0KCTxwYXRoIGZpbGw9IiNGMDUxMzMiIGQ9Ik05Mi43MSw0NC40MDhMNTIuNTkxLDQuMjkxYy0yLjMxLTIuMzExLTYuMDU3LTIuMzExLTguMzY5LDBsLTguMzMsOC4zMzJMNDYuNDU5LDIzLjE5DQoJCWMyLjQ1Ni0wLjgzLDUuMjcyLTAuMjczLDcuMjI5LDEuNjg1YzEuOTY5LDEuOTcsMi41MjEsNC44MSwxLjY3LDcuMjc1bDEwLjE4NiwxMC4xODVjMi40NjUtMC44NSw1LjMwNy0wLjMsNy4yNzUsMS42NzENCgkJYzIuNzUsMi43NSwyLjc1LDcuMjA2LDAsOS45NThjLTIuNzUyLDIuNzUxLTcuMjA4LDIuNzUxLTkuOTYxLDBjLTIuMDY4LTIuMDctMi41OC01LjExLTEuNTMxLTcuNjU4bC05LjUtOS40OTl2MjQuOTk3DQoJCWMwLjY3LDAuMzMyLDEuMzAzLDAuNzc0LDEuODYxLDEuMzMyYzIuNzUsMi43NSwyLjc1LDcuMjA2LDAsOS45NTljLTIuNzUsMi43NDktNy4yMDksMi43NDktOS45NTcsMGMtMi43NS0yLjc1NC0yLjc1LTcuMjEsMC05Ljk1OQ0KCQljMC42OC0wLjY3OSwxLjQ2Ny0xLjE5MywyLjMwNy0xLjUzN1YzNi4zNjljLTAuODQtMC4zNDQtMS42MjUtMC44NTMtMi4zMDctMS41MzdjLTIuMDgzLTIuMDgyLTIuNTg0LTUuMTQtMS41MTYtNy42OTgNCgkJTDMxLjc5OCwxNi43MTVMNC4yODgsNDQuMjIyYy0yLjMxMSwyLjMxMy0yLjMxMSw2LjA2LDAsOC4zNzFsNDAuMTIxLDQwLjExOGMyLjMxLDIuMzExLDYuMDU2LDIuMzExLDguMzY5LDBMOTIuNzEsNTIuNzc5DQoJCUM5NS4wMjEsNTAuNDY4LDk1LjAyMSw0Ni43MTksOTIuNzEsNDQuNDA4eiIvPg0KPC9nPg0KPC9zdmc+DQo=
section:
  - name: Sign commits
    commands:
      Obtain your key: gpg --list-secret-keys --keyid-format long
      Set your key: "git config user.signingkey <long-key-id>"
      Tell git to sign all of your commits: git config commit.gpgsign true
      Also sign tags: git config tag.gpgsign true
  - name: SSH Keys
    commands:
      Clone with a different ssh key: git clone -c core.sshCommand="ssh -i ~/.ssh/your-ssh-fileName" git@github.com:orgname/repo.git
  - name: Revert/Undo
    commands:
      Revert last 3 commits: git revert --no-commit HEAD~3..
      Undo last local commit, but keep changes: git reset HEAD~
  - name: Prune remote branches
    commands:
      Only prune remote branches: git remote prune origin
      Update remote branches: git remote update origin --prune
      pull & prune: git pull --rebase --prune --autostash
      Always prune on fetch/pull globally: git config --global fetch.prune true
      Always prune on fetch/pull for current repo: git config remote.origin.prune true
  - name: List unpushed branches
    commands:
      git log: git log --branches --not --remotes --no-walk --decorate --oneline
      git branch: git branch -vv
  - name: cleanup
    commands:
      Delete local branch: git branch --delete branch-name
      Delete remote branch: git push --delete origin branch-name
      Find non-merged branches: git branch --remote --no-merged
      Delete merged local branches: git branch --merged origin/master | grep -v \* | xargs git branch -D
      Find largest files (even in history): "git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | sed -n 's/^blob //p' |   sort --numeric-sort --key=2 | cut -c 1-12,41- | $(command -v gnumfmt || echo numfmt) --field=2 --to=iec-i --suffix=B --padding=7 --round=nearest"
  - name: bundle
    commands:
      Complete repo: git bundle create (basename $PWD).git.bundle --all
  - name: List
    commands:
      Count commits per author: git shortlog --summary --numbered --email --no-merges [--all]
      Count commits per day: git log --date=short --pretty=format:%ad | sort | uniq --count
      Show all config entries with their origin: git config --list --show-origin
  - name: Stash
    commands:
      Stash with name: git stash push -m my-stash
      Apply changes to current branch (deletes the stash): git stash pop
      Apply and keep stash: git stash apply
      Apply by name: git stash apply stash^{/my-stash}
      List: git stash list
      Show filenames (most recent stash): git stash show
      Show changes (most recent stash): git stash show -p
      Show changes (specific stash): git stash show -p stash@{1}
      Show full filenames: git stash show -p stash@{0} --name-only
      Show diff of single file in stash: git diff stash@{0}^! -- file.txt
  - name: Filter commits
    commands:
      by Date and author: git lg --after={2016-09-01} --before={2016-10-01} --author="Andreas Mausch"
      since/until: git lg --since="2 year ago" [--until="3 weeks ago"]
      Diff from yesterday: git diff @{yesterday}..HEAD
  - name: Feature branches
    commands:
      Create new feature branch: git checkout -b my-feature main
      Create new empty branch: git checkout --orphan empty-branch
      Count commits on feature branch: git rev-list [--no-merges] --count origin/master..HEAD
      List commits on branch (use git log if alias is not set): git lg --left-right --graph --cherry-pick [--no-merges] origin/master..HEAD
      List commits on branch (via cherry): git cherry master FEAT-branch
      Table of all branches and their commit count compared to origin/master: git for-each-ref refs/heads refs/remotes/origin --format='%(refname:short)' | xargs -i sh -c 'ahead=$(git rev-list --count origin/master..{}); behind=$(git rev-list --count {}..origin/master); printf "%4s %4s {}\n" "+$ahead" "-$behind"'
      Merge branch without checkout (merge local dev into local master): git fetch . dev:master
      Check if a specific commit is part of a branch: git branch --contains 818a06f
  - name: Create patch
    commands:
      Specific commit: git format-patch -1 <hash>
      Unstaged changes: git diff
      Staged changes: git diff --staged
      Both (unstaged and staged) changes: git diff HEAD
      Multiple commits into single file: git format-patch origin/master..HEAD --stdout > commits.patch
      Apply multiple commits file: git am commits.patch
  - name: Changes between branches
    commands:
      Summary (filenames and amount of changes): git diff --compact-summary branch..master
    shortcuts:
      Jump to next file: <kbd>n</kbd>
      Jump to previous file: <kbd>N</kbd>
  - name: Encoding
    commands:
      Show umlauts in filenames: git config --global core.quotepath false
  - name: Default branch / Remote head
    commands:
      Find default branch: git symbolic-ref refs/remotes/origin/HEAD | sed 's@^refs/remotes/origin/@@'
      Update from remote: git remote set-head origin --auto
  - name: Debugging HTTP (for example HTTP 403 Forbidden) and SSH connections
    commands:
      HTTP: GIT_TRACE_CURL=true git pull
      HTTP (deprecated): GIT_CURL_VERBOSE=1 GIT_TRACE=1 git pull
      SSH: GIT_SSH_COMMAND="ssh -vvv" git pull
  - name: git gui
    shortcuts:
      Stage file: <kbd>CTRL</kbd>+<kbd>T</kbd>
      Unstage file: <kbd>CTRL</kbd>+<kbd>U</kbd>
      Revert file: <kbd>CTRL</kbd>+<kbd>J</kbd>
---

**Github: Search issues created or commented by me**

- [created](https://github.com/search?q=is%3Aissue+author%3A%40me)
- [commented](https://github.com/search?q=is%3Aissue+commenter%3A%40me)

**Replace wrong email after commits have been pushed**

```bash
git filter-branch --env-filter '
WRONG_EMAIL="wrong@example.com"
NEW_NAME="New Name Value"
NEW_EMAIL="correct@example.com"

if [ "$GIT_COMMITTER_EMAIL" = "$WRONG_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$NEW_NAME"
    export GIT_COMMITTER_EMAIL="$NEW_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$WRONG_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$NEW_NAME"
    export GIT_AUTHOR_EMAIL="$NEW_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

Keep in mind you might need to `git push --force` afterwards.
Please be aware of all the consequences of a force push.

**Push local repo to a remote url**

```bash
git remote -v # List remotes
git remote add origin <ssh-url> # e.g. git@gitlab.com:andreas-mausch/repo.git
git push -u origin --all
```

**My git aliases**

See [here](https://github.com/andreas-mausch/manjaro-post-installation-scripts/blob/801bf8b389f1fe1246117cf9978fe537da05e342/git/script.sh#L7-L15)
