# The 3 aera in git

- working area also named working tree
- staging area alse `the cached` or the `index`
- the repository

--

- working area
  - files that are not handling by git and not in staging , `untracked files`
- staging area
  - files that are going to be part of the next commit
- repository
  - files that git already know about, the one checked-in

## Staging area

a "clean" staging area isn't empty, the baseline of a staging area as being an exact copy of the latest commit

`git ls-files -s` list the files of staging

> how does git know when you have edited a files, `because the sha-1 of the new file is different from the old one`

- git add <file>
- git rm <file>
- git mv <file>

- git add -p
  - add commit in chunk interactively

When you checkout files from the staging area, you just replaceing your diff with the file in the repository, you're are not removing them

## git stash

there is one more place where git stores files, it's the stash

stash changes
➤git stash
➤list changes
➤git stash list
➤show the contents
➤git stash show stash@{0}
➤apply the last stash
➤git stash apply
➤apply a specific stash
➤git stash apply stash@{0}
➤Keep untracked files
➤git stash --include-untracked
➤Keep all files (even ignored ones!)
➤git stash --all

➤Keep untracked files
➤git stash --include-untracked
➤Keep all files (even ignored ones!)
➤git stash --all

➤Name stashes for easy reference
➤git stash save "WIP: making progress on foo"
➤Start a new branch from a stash
➤git stash branch <optional branch name>
➤Grab a single file from a stash
➤git checkout <stash name> -- <filename>
59

➤Remove the last stash and applying changes:
➤git stash pop
➤tip: doesn’t remove if there’s a merge conflict
➤Remove the last stash
➤git stash drop
➤Remove the nth stash
➤git stash drop stash@{n}
➤Remove all stashes
➤git stash clear
60

git stash -p

--
