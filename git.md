# Git snippets

## Create branch locally and push it to origin

```console
git checkout -b <branch_name>
git push -u origin <branch_name>
```

## Undo last commit

Soft, keep changes:

```console
git reset --soft HEAD~1
```

Hard, discard changes:

```console
git reset --hard HEAD~1
```

## Delete untracked files

```console
git clean -n  # Dry run
git clean -f  # Forced mode
```

## Rename a local and remote branch

Rename local branch:

```console
git branch -m <old-name> <new-name>
```

Delete the old-name remote branch and push the new-name local branch:

```console
git push origin :<old-name> <new-name>
```

Reset the upstream branch for the new-name local branch:

```console
git checkout <new-name>
git push origin -u <new-name>
```

## Squash last N commits and give them a new message

```console
git reset --soft HEAD~N && git commit
```

## Reset local commits to remote origin state

```console
git fetch origin
git reset --hard origin/<branch-name>
```

## Delete branch

### Delete local branch

Merged:

```console
git branch -d <branch_name>
```

Unmerged:

```console
git branch -D <branch_name>
```

### Delete remote branch

```console
git push origin --delete <branch_name>
```

## Provide a git identity for one-shot command

```console
git -c user.email=name@domain.com -c user.name='My Name' \
    <git_command>
```

## Change origin URL

```console
git remote set-url origin <origin_url>
```

## Delete local references to non-existing remote branches

```console
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

```console
git tag -l
```

Create a lightweight tag:

```console
git tag <tag_name>                      # current commit
git tag -a <tag_name> <commit_hash>     # existing commit
```

Get tag information:

```console
git show <tag_name>
```

Print the latest tag:

```console
git describe --tags --abbrev=0
```

By default, the git push command doesn't transfer tags to remote servers.
You will have to explicitly push tags to a shared server after you have created them.

```console
git push origin <tag_name>
```

Delete local tag:

```console
git tag -d <tag_name>
```

Delete remote tag:

```console
git push origin --delete <tag_name>
```

## Different user email per repository

```console
git config --local user.email <name@mail.com>
```

This command only affects the current repository. Any other repositories will still use the default email specified in
`~/.gitconfig`.

## Linear history with rebase

Too much hassle.
