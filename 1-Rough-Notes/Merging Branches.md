All you have to do is check out the branch you wish to merge into and then run the git merge command:

```
$ git checkout master
$ git merge hotfix
$ git branch -d hotfix   // deletes the branch after finishing with it
$ git checkout issue 99 
$ git merge master // to add newest updates to current branch if needed 
```

https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging
fast-forward merge 
no fast-forward merge 
