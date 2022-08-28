# Rebase and amend

amend -

rebase -
rebase = give a commit a new parent (ie new `base` commit)

TODO: add slides capture

rebase
1 - rewind HEAD, meaning change the head position
2 - replay my commit on top of HEAD

the power of rebase come from replaying commit

kinda like a fast-forward

in the rebase options there is also `drop`

We can also use rebase to split commit, into many commits

--
"amend any commit with fixup and autosquash"

if you `git commit --fixup <SHA?>`

`git rebase -i --autosquash <SHA?>^` will generate the right todo?

you don't have to do an interactive rebase if you just wan to modify one commit

to make a secure rebase, you just have to make a new branch, and use that ref a fallback if things go wrong
