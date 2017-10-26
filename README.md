# git-cheat-sheet

Cheet sheet of git commands

## Basics

Command                    | Description
-------------------------- | ---------------------------------------------------------------------------
`git clone <url>`          | Clone git repo at <url> into current working directory
`git status`               | Show the current state of the repo, including changed and uncommitted files
`git log`                  | Output the commit history
`git log --oneline`        | Same as above but one line for each commit and a shortened hash
`git log --pretty=oneline` | Same as above but with the full hash


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
