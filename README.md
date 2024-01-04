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
1) set proxy by copying these commands to terminal

	`git config --global http.proxy http://10.1.123.16:8888`

	`git config --global https.proxy http://10.1.123.16:8888`

2) set git credentials in credential manager (OKTA etc.) (for example when doing first clone from Aon Repo)

##############################
#### Example command flow ####
##############################

### Main branch to be edited only by point person ###
### For basic work - branches are used ###

### Example 1, Cloning existing repo and creating new personal branch ###
0) `cd [dir URL]`	   # go to directiory
1) `git clone [URL]`	   # clones to folder the URL copied from website
2) `git branch [BranchName]`	   # creates new branch
3) `git checkout [BranchName]`	   # switches to existing branch


### Example 2, Working in directiory on personal branch ###
1) `git checkout [BranchName]`    # go to personal branch to work
2) `git status`	   # see changes
3) `git add [Filename / Dir . / .]`    # adds files to staging area
4) `git commit -m 'message'`
5) `git push`    # uploads branch to remote repo 
6) here pull/merge request can be made for point person to review and merge into main


### Example 3, Merging Branches + Conflicts ###
1) `git checkout [branch-a]`	# edit fcs
2) `git commit -m 'msg'`
3) `git checkout [branch-b]` 	# edit fcs at same row
4) `git commit -m 'msg'`
5) `git checkout [branch-a]`	# checkout to branch to merge into
6) `git merge [branch-b]`	# branch to be merged
7) conflict happens - manual edit the change in the editor
8) `git commit -m 'msg'`	# commit after resolving conflict
9) `git branch -d [BranchName]`	# deletes branch if needed

