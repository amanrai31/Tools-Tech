## Github (git stash and git stash pop)
Suppose I am on main branch and i want the changes done by me on main branch to be transfered on some other branch, then-
- On main branch (or whatever branch it is i.e.- first branch)--- git stash
- Change your branch (go to the second one)
- git stash pop. 


## From fresh local to remote (Local => Remote) 

1. Create empty folder (Your application)
2. `git init`
3. `git add <filename>` OR `git add .` -add 1 or multiple files
4. `git commit -m "Commit message"`  - commit
5. Create remote repo in Github and copy the link.
6. `git remote add origin <link>` - adding remote repo in local application
7. `git remote -v` - varify remote has added successfully
8. `git push -u origin main` (Setting upstream for future) OR `git push origin main`
9. After 1st time- regular commands- `git add .` | `git commit -m "Commit message"` | `git push`

Note: `git status` - Untracked, Modified, Staged, Unmodified. 

Note: `git log` - For logs (History of commits-All HASH are there)

Note: `git diff <branchName>` - See diff between current branch and given branch

## From remote to local (Remote => local)

1. Create new repo
2. Go to target directory
3. `git clone <link>`
4. Write code, do changes.
5. `add` => `commit` => `push`

## Branching
1. `git branch <branchName>` - Creates new branch
2. `git checkout <branchName>` - Switch/checkout branch
3. `git branch -d <branchName>` - delete branch

## Merge (Using CLI, using PR)
Using CLI
1. `git checkout master` - Switch to master/main branch
2. `git merge <branchName>` -Merge another branch into master

Using PR => [ Create PR, Set target branch, Desciption & Context, Type of change(Bug/Feature), Testing tools, Reviewers and other IMP INFO]

## Merge Conflict
    
    
