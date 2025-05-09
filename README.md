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


### Branching strategy:
How to develop and how to release applications to production?

Git flow model: (old branchin strategy , widely used in monolythic apps). Its used no also in versioning applications which supports multiple versions at a time. Like whatsapp, android etc. Big application use this flow.

![image](https://github.com/user-attachments/assets/78f55074-f5b2-4f1f-a7f4-5ded6460cf3a)

Git flow usually have 2 long lived branches for life time (long lived means, these branches do not be deleted)
1. main
2. development

We also hve short lived branches in git flow
1. feature branch
2. release branch
3. hot fix branch

Every branch has source and destination. Source for development branch is main.

Similarly source for featue1 (say video call) is development branch. And destination for featue 1 is development. So feature branched comes from development and merges to development

Hotfix branches come from main (master) and merge to main and development branches.

Release branch come from development and merged to main and development.

Once the feature is developed and merged to development brach, then a release branch is created. And then testing happens (in UAT, QA etc), issues are fixed and then merged to development and main.

Hotfix means - emergencey change. 

Feature Branching model: 

For web applications / micro services git flow model is very heavy. So we use github flow or feature branching strategy.

feature branching model has 2 branches
1. main/master
2. feature

![image](https://github.com/user-attachments/assets/8cee856a-f37e-4185-8624-56adee164daf)

Usually one feature is developed by one person.

CICD process is run on feature branch. Build, scan, deploy in dev, functionality test -> this process ic called shift left process.

Shift left is important strategy in feature branching model. Shift left means, it includes scans, testing in early stages of development instead of after development.

Then the feature is deployed to main branch. Then this feature can be deployed to different environsments SIT, UAT, QA, pre-prod etc, i.e non-prod

Fianlly its deployed to prod through CR process.

git reset vs git revert: These are to undo the changes.

We have 3 areas in git
1. workspace area - this is where we make changes to files/code. (eg: VS code)
2. stageing area - when we run (git add . ) command files/changes added to staging area
3. commit area - changes are commited to git from staging area. (git commit -m "messages")

git reset: is used before we push to remote branches (non-main branches) . 3 options present in git reset

1. soft -  Changes will removed in commit area , but changes still exists in staging area.
2. mixed - (default option) - Changes will be removed in staging are, commit area. But it keeps changes in workspace.
3. hard - changes will removed from commit, staging and work space areas.
Assume we have 3 commits given with command git add .; git commit -m "". Last commit is called HEAD

To see git log with commits IDs in one line
```
git log --oneline
```
```
git reset --soft HEAD~1            (HEAD-1 means - removes the last commit)
git reset HEAD~1
git reset --hard HEAD~1
# To removes changes till some commit id
git reset --hard <commit-id>
```
So git reset removes the history and changes commit ID. So its not recommended to use in remote branches. We may use git reset in local branches. If we do reset in remote branches, then other users will be effected, if they are using it.


git revert: revert will not remove old commit IDs, it will add extra commit IDs. We get conflicts with revert. We need to correct the wrong commits. Commit history is not changed.
```
git revert HEAD~1
```

Git Cherry pick: 

When we find something useful in another branch, we can pick those commits instead of compeletey merge or rebase with that branch.

when we use git pull , it pulls latest from the branch we are in , we can use "gir pull origin main" to be specific to pull from main branch.

Assume 2 users working on same file. User1 made some changes to file in his own branch and committed multiple times then pushed to his branch. Then finally pushed to main branch by approvals.

Now user2 also made changes to the same file in his branch and committed multiple times and pushed to his branch. Then tried to push to main branch from approvasls, and he got conflicts. Then user2 sees what changes made in the main branch (git log main), and decided he wants to cherry pick a specific commit by using below command,
```
git cherry-pick <commit-id>
```
Now when he opens his file editor, it shows the newly cherry picked changes and his changes, then he modifies the changes accordingly,and then commits to his own branch now. After that tried to push to main branch, further he gets conflicts, then user2 solves the conflicts with
```
git merge main
```
After solving the conflicts, then he commits to his own branch then push to his branch. Then after review and approaval, user2 changes goes to main branch.

The above things shown cherrypick from main branch. Cherry pick can be done from other user's branches also (user2 can cherry-pick from user1 commits also).
```
git checkout user1
git pull
git checkout user2
git log user1
git cherry-pick <commit-id-of-user1>        # this may create conflicts, resolve and then commit and push.
```

Git restore:

Create a new branch for testing git restore. Make some changes in a file and commit to local branch. (means, $git add . ; git commit -m "message" )

Now make some changes and add changes to only staging area by using $git add .

Then check $git status   , it shows restore command as "$ git restore --staged <filename>"  to unstage the file. Now the cahnges are in staging and workspace area.

So before comminting these changes, if we want to correct, then we can unstage by using 
```
git restore --staged <filename>
git status
```
Now the changes are removed in staging area and changes exist in workspace.

We can restore to specifc commit also
```
git log --oneline
git restore --source=<commit-id> <file-name>
git log --oneline
```
It brings the changes of the above commit-id to workspace. But it wont delete the commit-ids. So restore command restores the file to particular commit-id, but it wont delete commit-ids

```
git pull origin main
git checkout <branch name>
Then do some changes in files. Now if we want to discard the changes we made and restore the workspace then,
git restore <file name>
```
So to discard uncommitted local changes in a file, we can use "git restore <file name>"

So in restore we have option to choose particular file. But in reset and revert, we do not have option to choose particular file, it effects on entire workspace.





