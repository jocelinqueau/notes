# Merge and rebasing

Undert the hood merge commit are just commit but they happens to be more than one parent. You can merge as many parent into a merge commit as you would like. It's more like a marker of when a new feature is introduce on the branch

--
fast-forward, what is that ?

it's happen in case there is no need to make a merge commit, there were no activity on the branch we merge on, or at least just moving the ref of the merge branch to the new commit of current branch is enough

The problem is you lose the clear delineator(delimiter) since there is no merge commit

you can specify, `git merge --no-ff`

--
merge conflict

during a merge conflict git is gonna generate new files to let you handle thoses conflicts

--
git rerere (reuse recorded resolution)

`git config rerere.enabled true` for the project
or
`git config --global rerere.enabled true` for all project
