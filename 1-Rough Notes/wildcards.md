##### **Wildcards**
Before we begin using our commands, we need to talk about a shell feature
that makes these commands so powerful. Because the shell uses filenames
so much, it provides special characters to help you rapidly specify groups
of filenames. These special characters are called **wildcards**.
![[6-Attachments/Screenshot from 2025-02-22 10-31-23.png]]


![[6-Attachments/Screenshot from 2025-02-22 10-32-04 1.png]]
    Range wild card touch file{ 1...3}.txt


	**Character Ranges**   <----- very important note 
If you are coming from another Unix-like environment or have been reading some other books on this subject, you may have encountered the [A-Z] and [a-z] character range notations. These are traditional Unix notations and worked in older versions of Linux as well. They can still work, but you have to be careful with them because they will not produce the expected results unless properly configured. For now, you should avoid using them and use character classes instead.
