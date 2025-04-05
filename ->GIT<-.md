
[[Books/GitHub.pdf|GitHub]]

‫‪Email ‫‪and‬‬ ‫‪username ‫‪Configure as an identifier for my local repository 

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



git add . ->  . means all files 
git add filename1 filename2 -> select specific files using git add they are transitioned to **staging area** 
meaning they are ready to be committed 

git commit -m "initial commit"  -> here the changes are are committed for the staged files this is called **committing area**

-m -> 

git log -> shows all versions of the directory i.e all commits done on it 
--name-only 
