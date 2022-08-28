# References, commit and branches

references are pointers to commit, type of refences are:

- tags, annotated tags
- branches
- HEAD

- what is a branch ?
  - just a pointer to a particuliar commit
    - which point to a tree ... etc
  - the pointer of the current current brnach, change as commit are made

- what is HEAD ?
  - HEAD is how git know what branch or commit we currently on
  - what is the parent a of the commit we are making

lighteight tag are just pointer to commit

`git tag <something>`
<!-- capture value of HEAD at the moment  -->

annotated tags, same as lightweifght tag but they do have message, date author

`git tag -a <> -m (optional)`

-
tag and branches

branch move everytime you make a commit, a tag don't it's a snapshot

--
