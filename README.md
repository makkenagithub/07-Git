# 07-Git

Git:
1. create repo
2. git clone
3. git add  -> staging area
4. git commit -m ""   -> commit to local repo
5. git push   -> push to central repo

Git is a distributed (de-centralized) version control system. 

1. git init    -> converts an existing folder to a git repo.  .git directory will be created. If we delete .git directory, then the folder becomes a normal folder (not git repo).
2. git remote add main <url>   -> 
3. git branch -M main    -> to change branch main.

The above is to push existing repo to git.

Branching:

main branch -> points to production.

We do not directly make changes to main branch. We create another branch from main branch. Do the changes. Test the changes, scan the changes. If everything is ok, then bring the changes to main branch.

This is total process.

Git has key value.

For every commint in git there is 40 character length SHA code (commit id) (eg:  efc683d22267af54c86c56480f571966d3ce8c88).

This SHA code (commit id) is key. Value is our code commited to git.

1. if the commit id is changed, then we can say code is changed.
2. if the code is changed, then commit id also changed.

Pull request rule setting:

Nobody can push changes to main branch directly. We can set the approvals by adding branch rule set.

Github -> go to a branch (eg: 07-git) -> settings -> branches -> Add branch rule set -> Require a pull request before merging (add approvers)

After the approval only the changes are pushed to main branch.

After adding rules, how to make changes?

Create another branch from main branch -> do changes -> create pull request (PR)-> get the approval -> merge changes. This is the procedure.

After cloning the url , we can see git log to get the commmit IDs

```
$ git log
commit 811624dfd09d5f338f9b125b54e891d8ecbb9d40 (HEAD -> main, origin/main, origin/HEAD)
Author: Suresh Makkena <58598378+makkenagithub@users.noreply.github.com>
Date:   Fri May 2 20:02:31 2025 +0530

    Create test.txt
```
To create another branch from main branch:
```
git checkout -b test-branch
$ git checkout -b test-branch
Switched to a new branch 'test-branch'

Rohan@LAPTOP-V3QJRG9P MINGW64 ~/OneDrive/desktop/suresh/devopsPractice/07-Git (test-branch)
$ ls -lrt
total 5
-rw-r--r-- 1 Rohan 197121    2 May  2 20:02 test.txt
-rw-r--r-- 1 Rohan 197121 2112 May  2 20:07 README.md

Rohan@LAPTOP-V3QJRG9P MINGW64 ~/OneDrive/desktop/suresh/devopsPractice/07-Git (test-branch)
$

```
In the about we checkout the code to new branch called test_branch. Then make some changes to the code in test.txt file. Then push the changes to test-branch as below

Then
```
git add . ; git commint -m "chnaged test.txt" ; git push origin test-branch
```

Then in github console, it appears that test-branch has recent pushes. Click on compare & pull request. Then it goes for approval as created in pull request rule setting , after approval, then click on merge pull request, so that changes go to main branch.

Here git creates merge commmit, as below

![image](https://github.com/user-attachments/assets/f4d11dda-fbee-4b4d-997e-0068efac0515)


Then to go to main branch in git bash
```
git checkout main
```
Every merge commit has 2 parent commits. To see the parent Ids
```
git cat-file <merge-commit-id> -p
```
Merge commit:
1. Every merge commit has 2 parent commits.
2. Merging preserves (maintains) all history. at any point we can track all history.
3. Merge commit is an extra commit created by git.
4. creates non-linear history

Rebase commit: 
1. rebase will not create extra commit (as like merge commit).
2. there is no history preserved in rebase commit.
3. commit IDs will be changed in rebase.
4. creates linear history

Merge is prefered if a branch is developed by multple people. To know who did what merge commit is prefered. To know history merge commit is prefered

Rebase is prefered, if a branch is developed by single person. If we do not want history, go for rebase. 

For eg, we get app development and made lot of changes sequentially to develop the app. Then if we want all history of changes, the merge commit is prefered, else rebase is prefered.

Merge conflicts:

Conflict comes when git finds different code in same line. Then git will give conflict. When 2 people are woking on same issue / feature, If person1 commited his changes to main branch, then later when person2 tries to commits his chnages to main branch , then merge conflict will come.

Resolving conflicts: both perosns need to discuss the changes and resolve conflicts. 

Person2 needs to go to main branch and get latest code and merge the new changes 
```
git checkout main
git pull
git checkout person2
git merge main
```
After merging the latest changes by person2, the if you open the file in vs code or notepadd++, the git shows changes by <<< and >>>> symbols with HEAD and main.

HEAD means the peroson who is working i.e. person2. main means existing change. Then discuss and decide by person1 and person2, then make the changes in the above opened file finally (i.e. removing <<< >>> symbols, HEAD, main etc and keep finalised content).

Then
```
git add . ; git commit -m "resolve conflict changes for issue/feature" ; git push origin person2
```
This is how merge conflicts can be resolved and then perosn2 can commit his changes to main branch from git console.




