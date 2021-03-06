


## Work with remote   

### Credential   
##### How to avoid being asked for password and username everytime I push?  
    git config credential.helper store
    git push https://github.com/repo.git

### Branch    
##### Fetch from remote branch  
    git checkout --track origin/daves_branch  |  git checkout -b [branch] [remotename]/[branch]

##### Change the branch name  
    git branch -m new_name
    
##### Check information of all branches
    git branch -vv
    
##### Check current branch's information
    git status -sb

##### Fetch just one branch
    git fetch origin branch_name


### Merge  
##### Merge all commits on issue1 branch to one commit and import it to the master branch
    git merge --squash issue1
    
### Collaboration
##### If work with others in the same branch, after each `force push`, we need to let others know and others need to do a `git reset --hard origin/branch_name` to sync with the force push. If you have any unstaged changes, make sure you stash them before doing that. If you have unpushed commit, you can do `git fetch` then `git rebase -i origin/branch_name` and only pick that unpushed commit.

##### 不要用 git push --force，而要用 git push --force-with-lease 代替。在你上次提交之后，只要其他人往该分支提交给代码，git push --force-with-lease 会拒绝覆盖。

##### If you want to find out who is the author of the file, try `git blame PATH_TO_THE_FILE`.

### Checkout   
##### With branch specifier only (`git checkout branch`) it will switch current working directory to specified branch, keeping local changes if possible and failing otherwise. If you already are on branch, it will do nothing at all. It only modifies files in the working directory that differ between  HEAD and branch and fails if any of them has local modifications (indexed or not).
##### With path specifier only (`git checkout .`) it writes content from index. That it is undoes unstaged local modification. To undo staged modifications, use git reset with path specifier.
##### With both branch and path specifiers (`git checkout branch .`) it writes content in specified revision. It will not modify where HEAD points, so if branch is different from HEAD, there will be staged changes afterwards. And if you have unstaged or staged changes in the previous branch, it will be gone.  

### Cherry pick

##### How to cherry pick a commit from another git repository  

        cd /home/you/projectA
        git remote add projectB /home/you/projectB
        git fetch projectB
        git cherry-pick <first_commit>..<last_commit>
        
##### Check remote repos status

        git remote -v
        
##### Remove a remote repo

        git remote rm NAME

### Conflicts

##### Change some config to make things better

    git config merge.conflictstyle diff3 // this will show you the base, local and remote; 
    BASE is the common ancestor(s) of LOCAL and REMOTE

## Work locally  

### Stash   

##### Stash all changes including staged changes  
    git stash -u 
##### Stash all unstaged changes
    git stash -k 
##### Pop the last stash and remove it
    git stash pop 

### Reset  

##### Reset the HEAD to the previous commit  
    git reset --hard HEAD~
##### Reset back to the original version  
    git reset --hard ORIG_HEAD
##### Undo a commit and make the last commit to unstaged changes  
    git reset HEAD~
##### When you are one step behind the remote one, and you want to sync with it  
    git reset --hard origin/bugfix/DS-xxxx
##### When you do reset, you have 3 choices: --hard, --soft and nothing: 
    git reset --hard HEAD~ will let you go back to the previous commit, and the previous latest commit will be gone;
    git reset --soft HEAD~ will let you go back to the previous commit, and the previous latest commit will become staged changes;
    git reset HEAD~ will let you go back to the previous commit, and the previous latest commit will become unstaged changes.
    
### Rebase

##### amend to an older commit
    git rebase -i HEAD^^^
    choose the commit you want to amend, change `pick` to `edit`
    do your changes, add them, git commit --amend --no-edit
    git rebase --continue
    
##### Remove the merge commit  
    git rebase -i <sha of the commit before the diverge>
    then it will remove the merge commit

    
### Search in the history  

##### Search what happened inside a folder or a file: 
    git log -- xxx/xxx/xxx/aaa  |  git log -- xxx/xxx/xxx/abc.java
    
##### Search for a specific commit in the history.
    git log --all --grep='XXXXX'
    
    
### diff

##### git diff
    after git diff, you can save the diff file: git diff sha1 sha2 > aaa.diff
    then you can do git apply aaa.diff to add the difference to your branch
    
    
### commit

##### accidentally staged a file change in a commit, how to remove it from commit?
    git reset --soft HEAD^
    git reset HEAD pathToThatFile
    git commit -c ORIG_HEAD
    
##### When you do `git reset HEAD~` to reset the top commit, your commit message is gone as well. 
    If you want to reuse that commit message when you commit, do `git commit -C HEAD@{x}` (The number in {} depends on your `git reflog`, usually it's `1`)
    
