[[Merging Branches]]

creating a new branch 
branches are just pointer to a certain commit
git checkout -b sarah -> create new branch and switch to it (-b)
git branch sarah -> only creates a new branch 
git checkout sarah -> switches to the new branch 
git branch -> list all branches 

> [!NOTE]
> Before you commit your changes reside on disk (the "working copy") or after you git add the "staging area". Neither of these belong to a particular branch. When you switch branches, uncommitted changes will go with you. If changing a branch would overwrite your uncommitted changes, Git will not let you switch.
> 
> When you have work in progress and want to switch branches you should put it in the stash using git stash. See Stashing and Cleaning in Pro Git.
> 
> Alternatively you can commit your work in progress and then later use git commit --amend to add to the commit. See Rewriting History in Pro Git


HEAD points to the last commit on the branch you are already on by default , the HEAD moves with you on switching between branches 

`git checkout branch`
**This is an important point to remember: when you switch branches, Git resets your working directory to look like it did the last time you committed on that branch. It adds, removes, and modifies files automatically to make sure your working copy is what the branch looked like on your last commit to it.**

Branch life cycle :
	working on certain issue 
	commit 
	reviewing and testing 
	merge 
	delete the branch 




