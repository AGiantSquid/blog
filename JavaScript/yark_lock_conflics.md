If you yarn add a dependency to the project, or if you change a dependency in the package.json file and then run yarn setup, you will be changing either the yarn.lock file or the client/yarn.lock file. If another developer has also changed this file, you may experience a merge conflict when you attempt to push up your branch. Manually fixing this conflict will make you want to die. What you should do instead:


```bash
# If you tried merging develop into your branch, and got the message about merge conflict, abort the merge
git merge --abort
 
# First re-checkout the yarn.lock files from develop.
yarn checkout develop -- yarn.lock client/yarn.lock
 
# Next, install your dependencies. This will modify the file directly from develop, which will prevent conflicts!
yarn setup
 
# Commit your new yarn.lock files.
git commit -m 'fix yarn lock files'
 
# Push your files and behold, no conflicts!
git push
```