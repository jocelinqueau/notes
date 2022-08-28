# Fixing mistakes

- git checkout to redo

--
git clean
`git clean -f -d --dry-run` f files d directiories, default is fd i think, dry-run to show impact without doing it

git reset (git checkout only move HEAD, git reset move BRANCH too)

if you don't give it a HEAD pointer it's only modifie files

git reset (--mixed default) will .. take screen of slides there are better

--
git revert is the safe reset, what if you need to undo changes that are shared, you pushed it. git revert is going to create a commit to reverse (new commit with opposite changes )

--
