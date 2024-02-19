###########################
### Git Tutorial basics ###
###########################

#### Links ####
install git console from:
https://git-scm.com/downloads

command overview:
https://education.github.com/git-cheat-sheet-education.pdf

Easy to understand useful video tutorials:
https://www.youtube.com/watch?v=HVsySz-h9r4&list=PL-osiE80TeTuRUfjRe54Eea17-YfnOOAx


#### Must do steps after installation ####
1) set proxy by copying these commands to terminal (Prague only proxy)

	`git config --global http.proxy http://10.1.123.16:8888`

	`git config --global https.proxy http://10.1.123.16:8888`

2) set git credentials in credential manager (OKTA etc.) (for example when doing first clone from Aon Repo) - behaviour is rather unpredictable, sometimes multiple logins needed, sometimes login needed after each push/pull... If that does not work, generate one time password in DevOps. Near the clone button.


##############################
#### Example command flow ####
##############################


### Main (Master) branch to be edited only by PROJECT person ###
#### For basic work - branches are used ####

##############################

### Example 1, Cloning existing repo and creating new personal branch ###
0) `cd [dir URL]`	   # go to directiory
1) `git clone [URL]`	   # clones repos to folder from the URL copied from website
2) `git branch [BranchName]`	   # creates new branch
3) `git checkout [BranchName]`	   # switches to existing branch
4) `git push -u origin [BranchName]`	# first push of newly created branch

### Example 2, Working in directiory on personal branch ###
1) `git checkout [BranchName]`    # go to personal branch to work
2) `git status`	   # see changes
3) `git add [Filename / Dir . / .]`    # adds files to staging area
4) `git commit -m 'message'`
5) `git push`    # uploads branch to remote repo (if it exists on remote repo, if not use `git push -u origin [BranchName]`)
    After pushing, pull/merge request can be made for point person to review and merge into main on the DevOps website


### Example 3, Merging Branches + Conflicts ###
1) `git checkout [branch-a]`	# edit 01_math_fcs.py
2) `git commit -m 'msg'`
3) `git checkout [branch-b]` 	# edit 01_math_fcs.py at same row
4) `git commit -m 'msg'`
5) `git checkout [branch-a]`	# checkout to branch to merge into
6) `git merge [branch-b]`	# branch to be merged
    ##### conflict happens - manual edit the change in the editor
7) `git commit -m 'msg'`	# commit after resolving conflict
8) `git branch -d [BranchName]`	# deletes branch if needed

### Example 4, Fixing common mistakes ###
#### Example 4.1, Fixing bad commit message !BEFORE! pushing to remote ####
1) `git add [Filename]`
2) `git commit -m 'Wrong commit message'`
3) `git commit --amend -m 'Correct commit message'` 

#### Example 4.2, forgetting to commit a file that was supposed to be part of last commit without any other change in message etc. !BEFORE! pushing ####
1) `git add [forgotten file]`
1) `git commit --amend --no-edit`

#### Example 4.3, accidental commiting to Main instead of Branch - Moving commit to Branch and going a commit back on Main ####
1) `git log` # copy last commit hash written after 'commit' eg. smth like "c0d640e9f2642bd8fe3c3038e372433141aba4a0"... (first 7 chars are enough) press `wq` after to get out of log menu
2) `git checkout [BranchName]`
3) `git cherry-pick [Hash]` # transfers commit from Main to Branch
    ##### Possible manual conflict changes, commit new changes per Example 3
4) `git checkout Main` # go back to Main
5) `git log` # copy hash of previous commit you want to get back to
    ##### Here are 3 options to reset a) Soft b) Mixed c) Hard
6) `git reset --soft [Hash]` # gets back to previous state BEFORE commit with change already added to staging
6) `git reset [Hash]` # gets back to previous state BEFORE commit with change kept but not added to staging (default)
6) `git reset --hard [Hash]` # get back to previous state BEFORE commit, changes completely deleted from Main
    ##### All three resets DO NOT affect untracked files
7) `git clean -df` # gets rid of all untracked directories and files
