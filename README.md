# git-cheat-sheet

Cheet sheet of git commands

## Basics

Command                    | Description
-------------------------- | ---------------------------------------------------------------------------
`git clone <url>`          | Clone git repo at <url> into current working directory
`git status`               | Show the current state of the repo, including changed and uncommitted files
`git log`                  | Output the commit history
`git log --oneline`        | Same as above but one line for each commit and a shortened hash
`git log --pretty=oneline` | Same as above but outputs the full hash


## Branching

Command                                   | Description
----------------------------------------- | --------------------------------------------------------------------------------------
`git branch -v`                           | List the currently available branches.
`git branch <branch name>`                | Create a new branch from current working tree.
`git checkout <branch name>`              | Switch to a different branch.
`git checkout -b <branch name>`           | Create a new branch and immediately switch to it.
`git branch -d <branch name>`             | Delete a branch (will not delete if it hasn't been merged in)
`git branch -D <branch name>`             | Equivalent to `git branch --delete-force`
`git push -d <remote name> <branch name>` | Delete a remote branch
`git push <remote name> <branch name>`    | Push to a remote branch, will publish a new remote branch if one doesn't already exist


## Stashing changes

Command                      | Description
---------------------------- | ----------------------------------------------------------------------------------
`git stash`                  | Create a stash of the currently modified tracked files and staged changes
`git stash save "<message>"` | Create an annotated stash with a message
`git stash list`             | List all stashes currently on the stack
`git stash apply`            | Apply the most recently created stash to the currently checked out branch
`git stash apply stash@{n}`  | Apply the stash at position _n_
`git stash pop`              | Apply the most recently created stash then delete it. _(Optional stash@{n} param)_
`git stash clear`            | Delete all stashes on the stack
`git stash drop`             | Delete the stash on the top of the stack. _(Optional stash@{n} param)_

## Tagging

Command | Description
------- | -----------
`git tag` | List all the current tags
`git tag -l "<pattern>"` | Search for a tag with a wildcard search _e.g. v1.8.\*_
`git show-ref --tags` | List all tags with the commit they point to
`git tag -a <tag> -m "<message>"` | Created an annotated tag
`git tag -a <tag> -m "<message>" <hash>` | Create an annotated tag pointing to a specific hash
`git tag <tag>` | Create a lightweight tag _(does not include tagger info or message)_
`git push origin <tag>` | Publish a tag to remote named origin
`git push origin --tags` | Publish all tags to remote named origin
`git tag --delete <tag>` | Delete a local tag
`git push origin :<tag>` | Delete a remote tag _(pushes empty reference to remote tag)_
`git push --delete origin <tag>` | Delete a remote tag, more expressive than above


## Uh-oh

### Remove all traces of a file from git history

If you've accidentally added a file to the repo that should not be there, e.g. security related files, user names/passwords, etc, and have made several commits since adding the file, the `git filter-branch` command can be your friend.

`git filter-branch --index-filter 'git rm --cached --ignore-unmatch <filename>'`

The `--ignore-unmatch` in the inner command means that git won't fail if the given filename is missing from any given change.
You can optionally use `--tree-filter` instead of `--index-filter`. `--index-filter` is very similar to `--tree-filter` except that it does not check out the tree, giving a performance boost.

[filter-branch man page](https://gitirc.eu/git-filter-branch.html)


### Change author name/email for all commits

`git filter-branch -f --env-filter "GIT_AUTHOR_NAME='Bryce Jech'; GIT_AUTHOR_EMAIL='bryce@brycejech.com'; GIT_COMMITTER_NAME='Bryce Jech'; GIT_COMMITTER_EMAIL='bryce@brycejech.com';" HEAD`

## Troubleshooting

### Permissions

If getting a 404 when attempting to push to a repo, it may be that you don't have permission or that the repo is simply not configured properly.

If you do not have the ability to use ssh, you can modify the remote reference url to include your username and, optionally, your password. Note that if you must use an `@` symbol in your username, it must be URL encoded as `%40`. All special characters in the username/password string should be safely URL encoded.

`git remote set-url origin https://username@github.com/path/to/repo.git`

To include your password (not recommended) the command would look like this:

`git remote set-url origin https://username:password@github.com/path/to/repo.git`
