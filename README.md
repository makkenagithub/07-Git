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

Create another branch from main branch -> do changes -> cretae pull request (PR)-> get the approval -> merge changes. This is the procedure.



