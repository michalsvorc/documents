# Git

- [Pro Git e-book](https://git-scm.com/book/en/v2)
- [The Git Merge Handbook](https://www.freecodecamp.org/news/the-definitive-guide-to-git-merge/)

## Create branch locally and push it to origin

```shell
git checkout -b <branch_name>
git push -u origin <branch_name>
```

## Revert changes

### Undo last commit

Soft, keep changes:

```shell
git reset --soft HEAD~1
```

Hard, discard changes:

```shell
git reset --hard HEAD~1
```

### Delete untracked files

```shell
git clean -n  # Dry run
git clean -f  # Forced mode
```

### Revert unstaged changes to a specific file

```shell
git restore <file>
```

## Rename a local and remote branch

Rename local branch:

```shell
git branch -m <old-name> <new-name>
```

Delete the old-name remote branch and push the new-name local branch:

```shell
git push origin :<old-name> <new-name>
```

Reset the remote branch for the new-name local branch:

```shell
git checkout <new-name>
git push origin -u <new-name>
```

## Squash last N commits and give them a new message

```shell
git reset --soft HEAD~N && git commit
```

## Reset local commits to remote origin state

```shell
git fetch origin
git reset --hard origin/<branch-name>
```

## Delete branch

### Delete local branch

Merged:

```shell
git branch -d <branch_name>
```

Unmerged:

```shell
git branch -D <branch_name>
```

### Delete remote branch

```shell
git push origin --delete <branch_name>
```

## Provide a git identity for one-shot command

```shell
git -c user.email=name@domain.com -c user.name='My Name' \
    <git_command>
```

## Change origin URL

```shell
git remote set-url origin <origin_url>
```

## Delete local references to non-existing remote branches

```shell
git remote prune origin [--dry-run]
```

## .gitignore exclude folder but include specific subdirectory

```
# .gitignore

/dir-to-ignore/*
!/dir-to-ignore/subdir-to-keep/
```

## Tags

List all tags:

```shell
git tag -l
```

Create a lightweight tag:

```shell
git tag <tag_name>                      # current commit
git tag -a <tag_name> <commit_hash>     # existing commit
```

Get tag information:

```shell
git show <tag_name>
```

Print the latest tag:

```shell
git describe --tags --abbrev=0
```

By default, the git push command doesn't transfer tags to remote servers.
You will have to explicitly push tags to a shared server after you have created them.

```shell
git push origin <tag_name>
```

Delete local tag:

```shell
git tag -d <tag_name>
```

Delete remote tag:

```shell
git push origin --delete <tag_name>
```

Rename a lightweight tag:

https://stackoverflow.com/questions/1028649/how-do-you-rename-a-git-tag

## Different user email per repository

```shell
git config --local user.email <name@mail.com>
```

This command only affects the current repository. Any other repositories will still use the default email specified in
`~/.gitconfig`.

## Set up upstream branch to another repository

Note! Repositories generated from github templates behave differently than traditional forks.
Read [more](https://stackoverflow.com/questions/56577184/github-pull-changes-from-a-template-repository).

```shell
git remote add upstream <upstream-repo-url>
git fetch upstream [branch]
git remote show upstream
```

See last commit of local and remote branches:

```shell
git branch -av
```

Merge changes from upstream:

```shell
git merge upstream/<branch>
```

## Linear history with rebase

Too much hassle.

## Merge conflicts

`git mergetool`

### Accept all changes

- https://stackoverflow.com/questions/10697463/resolve-git-merge-conflicts-in-favor-of-their-changes-during-a-pull#answer-33569970

If you're already in conflicted state:

```shell
git checkout --theirs|--ours <file>
git add <file>
```

Use `.` when you want to accept everything.

## Submodules

### Download submodules added in upstream

```shell
git submodule init
git submodule update
```

### Add a submodule to existing repository

```shell
git submodule add <repository-url> [submodule/path]
```

### Fetch the latest changes from the submodule’s upstream repository

```shell
git submodule update --remote --merge
```

### Remove submodule

1. Remove the submodule entry from `.gitmodules`
2. `git submodule deinit -f path/to/submodule`
3. `git rm -f path/to/submodule`
4. `rm -rf path/to/submodule`
5. `git commit -m "Remove submodule path/to/submodule"`
6. `git clean -fd`

## Single branch

### Clone single branch

```shell
git clone <URL> --branch=<branch_name> --single-branch
```

### Clone additional branch in single branch repository

```shell
git fetch origin <another_branch>
git checkout FETCH_HEAD -b <another_branch>
```

- [source](https://stackoverflow.com/questions/70392689/clone-another-branch-after-cloning-single-branch)
