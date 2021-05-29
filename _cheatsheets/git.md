---
layout: cheatsheet
tags: vcs bundle
logo: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4NCjwhLS0gR2VuZXJhdG9yOiBBZG9iZSBJbGx1c3RyYXRvciAxNi4wLjAsIFNWRyBFeHBvcnQgUGx1Zy1JbiAuIFNWRyBWZXJzaW9uOiA2LjAwIEJ1aWxkIDApICAtLT4NCjwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+DQo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4Ig0KCSB3aWR0aD0iOTdweCIgaGVpZ2h0PSI5N3B4IiB2aWV3Qm94PSIwIDAgOTcgOTciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDk3IDk3IiB4bWw6c3BhY2U9InByZXNlcnZlIj4NCjxnPg0KCTxwYXRoIGZpbGw9IiNGMDUxMzMiIGQ9Ik05Mi43MSw0NC40MDhMNTIuNTkxLDQuMjkxYy0yLjMxLTIuMzExLTYuMDU3LTIuMzExLTguMzY5LDBsLTguMzMsOC4zMzJMNDYuNDU5LDIzLjE5DQoJCWMyLjQ1Ni0wLjgzLDUuMjcyLTAuMjczLDcuMjI5LDEuNjg1YzEuOTY5LDEuOTcsMi41MjEsNC44MSwxLjY3LDcuMjc1bDEwLjE4NiwxMC4xODVjMi40NjUtMC44NSw1LjMwNy0wLjMsNy4yNzUsMS42NzENCgkJYzIuNzUsMi43NSwyLjc1LDcuMjA2LDAsOS45NThjLTIuNzUyLDIuNzUxLTcuMjA4LDIuNzUxLTkuOTYxLDBjLTIuMDY4LTIuMDctMi41OC01LjExLTEuNTMxLTcuNjU4bC05LjUtOS40OTl2MjQuOTk3DQoJCWMwLjY3LDAuMzMyLDEuMzAzLDAuNzc0LDEuODYxLDEuMzMyYzIuNzUsMi43NSwyLjc1LDcuMjA2LDAsOS45NTljLTIuNzUsMi43NDktNy4yMDksMi43NDktOS45NTcsMGMtMi43NS0yLjc1NC0yLjc1LTcuMjEsMC05Ljk1OQ0KCQljMC42OC0wLjY3OSwxLjQ2Ny0xLjE5MywyLjMwNy0xLjUzN1YzNi4zNjljLTAuODQtMC4zNDQtMS42MjUtMC44NTMtMi4zMDctMS41MzdjLTIuMDgzLTIuMDgyLTIuNTg0LTUuMTQtMS41MTYtNy42OTgNCgkJTDMxLjc5OCwxNi43MTVMNC4yODgsNDQuMjIyYy0yLjMxMSwyLjMxMy0yLjMxMSw2LjA2LDAsOC4zNzFsNDAuMTIxLDQwLjExOGMyLjMxLDIuMzExLDYuMDU2LDIuMzExLDguMzY5LDBMOTIuNzEsNTIuNzc5DQoJCUM5NS4wMjEsNTAuNDY4LDk1LjAyMSw0Ni43MTksOTIuNzEsNDQuNDA4eiIvPg0KPC9nPg0KPC9zdmc+DQo=
section:
  - name: Sign commits
    commands:
      Obtain your key: gpg --list-secret-keys --keyid-format LONG
      Set your key: "git config user.signingkey <key>"
      Tell git to sign all of your commits: git config commit.gpgsign true
  - name: cleanup
    commands:
      Delete merged local branches: git branch --merged origin/master | grep -v \* | xargs git branch -D
      Update remote branches: git remote update origin --prune
  - name: bundle
    commands:
      Complete repo: git bundle create repo.bundle --all
  - name: Filter commits
    commands:
      by Date and author: git lg --after={2016-09-01} --before={2016-10-01} --author="Andreas Mausch"
      since/until: git lg --since="2 year ago" [--until="3 weeks ago"]
  - name: Feature branches
    commands:
      Count commits on feature branch: git rev-list [--no-merges] --count origin/master..HEAD
      Table of all branches and their commit count compared to origin/master: git for-each-ref refs/heads refs/remotes/origin --format='%(refname:short)' | xargs -i sh -c 'ahead=$(git rev-list --count origin/master..{}); behind=$(git rev-list --count {}..origin/master); printf "%4s %4s {}\n" "+$ahead" "-$behind"'
  - name: git gui
    shortcuts:
      Stage file: <kbd>CTRL</kbd>+<kbd>T</kbd>
      Unstage file: <kbd>CTRL</kbd>+<kbd>U</kbd>
      Revert file: <kbd>CTRL</kbd>+<kbd>J</kbd>
---

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

```bash
git config --global alias.lg "log --abbrev-commit --decorate --date=format:'%Y-%m-%d %H:%M:%S' --format=format:'%C(blue)%h%C(reset) %C(dim white)%ad%C(reset) %C(green)%<(8,trunc)%an%C(reset)%C(yellow)%d%C(reset) %C(white)%s%C(reset)'"
git config --global alias.tidy.branches "! git branch --merged origin/master | grep -v \* | xargs --no-run-if-empty git branch -D && git remote update origin --prune"
git config --global alias.tidy.tags "! git tag -l | xargs git tag -d && git fetch --tags"
git config --global alias.tidy "! git tidy.branches && git tidy.tags"
git config --global alias.first "hash-object -t tree /dev/null"
git config --global alias.tags "lg --tags --no-walk"
git config --global alias.branches "! git for-each-ref refs/heads refs/remotes/origin --format='%(refname:short)' | xargs -i sh -c 'ahead=\$(git rev-list --count origin/master..{}); behind=\$(git rev-list --count {}..origin/master); printf \"%4s %4s {}\n\" \"+\$ahead\" \"-\$behind\"'"
```

Example usage:

```
git lg origin/master..HEAD
```
