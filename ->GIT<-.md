
[[Books/GitHub.pdf|GitHub]]
[[HEAD^ and HEAD~ in git]]

git manual page
git help config 
git help log 

‫‪Email ‫‪and‬‬ ‫‪username ‫‪Configure as an identifier for my local repository i.e for every directory tracked by GIT

o understand Git configuration, you should know that:

> # Git configuration variables can be stored at three different levels. Each level overrides values at the previous level.

**1. System level (applied to every user on the system and all their repositories)**

- to view, `git config --list --system` (may need `sudo`)
- to set, `git config --system color.ui true`
- to edit system config file, `git config --edit --system`

**2. Global level (values specific personally to you, the user).**

- to view, `git config --list --global`
- to set, `git config --global user.name xyz`
- to edit global config file, `git config --edit --global`

**3. Repository level (specific to that single repository)**

- to view, `git config --list --local`
- to set, `git config --local core.ignorecase true` (`--local` optional)
- to edit repository config file, `git config --edit --local` (`--local` optional)

> # How do I view **all** settings?

- Run `git config --list`, showing **system**, **global**, and (if inside a repository) **local** configs
- Run `git config --list --show-origin`, also shows the origin file of each config item

> # How do I read one particular configuration?

- Run `git config user.name` to get `user.name`, for example.
- You may also specify options `--system`, `--global`, `--local` to read that value at a particular level.

git config --global user.name "koks"
git config --global user.email "kmagdyashour@gmail.com"

to validate my credentials 
git config user.name 
git config user.email
git config --list 


git command --> list all possible switches that git uses to perform its actions 

Repository two types 
local 
remote repository (GitHub)

working area -> staging area -> commit area 


git init -> initialize local repository at current directory creates a .git directory it handles all the version control history and contains metadata needed for the GIT to work 

git status -> shows the repository status shows the un-tracked files it also shows your current branch and commits 

any red file is not tracked and considered under the  **working area**  
any green file means its being tracked and under the **staging area**


git add . ->  . means all files 
git add filename1 filename2 -> select specific files using git add they are transitioned to **staging area** 
meaning they are ready to be committed 

git commit -m "initial commit"  -> here the changes are are committed for the staged files this is called **committing area**

> [!NOTE]
> ***commits message must atomic meaning that every commit should be dedicated to a certain part of the code or project instead of having multiple commits that contribute to the same thing and when i say on thing it can be multiple changes and files added/removed all to severe our purpose and to solve the part under-work***

-m -> message should be concise short and meaningful to reflect the updates happened on the files in staging area 

git log -> shows all versions of the directory i.e all commits done on it 
--name-only 
--oneline
it also shows all commits hash ID every commit has a specific HASH ID that refers to it 


git checkout hash_ID    -> head points to another commit on the master branch in this case using **git status** it shows something called head detached at *some hash id probably will be of the first master branch commit* in this detached mode Iam not on any branch up in the air 












### Understanding detached HEAD??

- **Detached HEAD state**: You enter this state when you check out a specific commit rather than a branch. In this mode, `HEAD` points directly to a commit, not to a branch reference.
    
- **Git Detached HEAD meaning**: Being in a detached HEAD means you're no longer working on the tip of a branch. Any commits made in this state aren't attached to any branch, making them harder to find later.

Identifying a detached HEAD

- **Check to see if you are in a detached HEAD state**: Run `git status`. If you're in a detached HEAD state, Git will explicitly tell you so.

Exiting detached HEAD state

1. **Go Back to Previous Branch**: If you simply want to exit detached HEAD state without keeping any changes made:
    
    `git checkout <branch-name>`
    
    Replace `<branch-name>` with the name of the branch you wish to return to, such as `master` or `main`. For more information, see this guide on [how to use git checkout](https://graphite.dev/guides/git-checkout-commit).
    
2. **Create a new branch from detached HEAD**: To keep your current changes, and continue working on them run:
    
    `git checkout -b new-branch-name`
    
    This command creates a new branch from your current detached HEAD position and switches to it. On this branch you can continue to push, pull, and commit as normal.
    

**Fixing a detached HEAD**

- **After accidental detachment**: If you've made commits in the detached HEAD state and want to attach them to a branch: Replace `<target_branch>` with your target branch . This sequence of commands creates a temporary branch pointing to your detached HEAD, then merges these changes back into your target branch so you can continue development as usual.

Terminal
``` bash 
git branch temp-branch
git checkout <target_branch>
git merge temp-branch
```





