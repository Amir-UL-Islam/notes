**.gitignore** only ignores newly added (untracked) files.

If you have files that have already been added to the repository, all their changes will be tracked as usual, even if they are matched by .gitignore rules.

To remove that folder from the repository (without deleting it from disk), do:

`git rm --cached -r .idea`