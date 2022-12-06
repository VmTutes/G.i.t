# Git
VmTutes Git
*********** GIT ************

Git Index:
==========

* What is SCM/VCS
* Introduction to GIT??
* Installing Git in Windows?
* Installing Git in Linux?
* Diff b/w Git and other tools
* What is Distributed version control system
* Architecture of git
* Stages in git
* Frequently used Terminologies
* Git global configurations
* Repo's
* log Management
* Git ignore concept 
* Branching
* Merging vs rebase
* Merge Conflicts
* cherry-pick
* snapshort
* stash
* Git Diff
* Undoís from working, staging, and committing areas
* HEAD 
* Tags
* rewritting commit messages

Git is a Source Code Management(SCM) / Version Control system(VCS) / Distributed version control  system

--> Types of SCM/VCS tools 
	* Git,
	* CVS,
	* Perforce,
	* clearcase,
	* svn

git:- it is a process of tracking and controlling/maintaining changes of a software product.

--> Download git from https://git-scm.com/
    which git --> path of git where it installed
    git --version -->to verify 
    git help config

Git Installation In EC2
------------------------
1. yum update -y
2. yum install git -y
   (Note:- here you will get old version of git)
3. yum remove git -y
   Note:- In case you need to install a specific Git version on your RHEL 8 system then use the below steps to compile and install Git from a source code.
4. to install latest version, for that you need to install some dependencys first.
   sudo yum install wget unzip tar make autoconf libcurl-devel expat-devel gcc gettext-devel openssl-devel perl-devel zlib-devel -y

5. Download the Git source code package from official website.
    wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.38.1.tar.gz

6. Extract the tar ball 
     tar -xvzf git-2.38.1.tar.gz

7. create folder in /opt/VmTutes

8. enter into extracted folder i.e git-2.38.1
     cd git-2.38.1

9. select where to install git. (by default it will go to /usr/bin/local)
     sudo ./configure --prefix=/opt/VmTutes

10. sudo make
11. sudo make install
12. git --version 
    ln -s /opt/VmTutes/bin/git /bin/git
    
git features compare to other tools:-

	1. Speed
	2. Support for non-linear development(thounds of branches, for parallel development)
	3. Able to handle large-scale projects.
     4. distributed version control system

Why Git is Distributed Version Control system:- 
	1. Speed
	2. Network Issues
	3. user collabration
     4. security reasons user to user sharing is not recommanded.


Git Terminology:-
=================
1. client/server
2. workspace: - space where the client comm with server
3. Repository : - it is a container/Directory. for each product/project we've one repository in the server.
4. Branch :- parallel development
5. Checkin:- Once the changes done, storing back to the server to maintain perminentaly
6  Checkout:- Taking petmission from server to do modifications.	
7. Revision/Version id/commit id : - git will track all the info of changes done by a user like when,which repo,who,which file, what changes) 

it stores in the form of snapshots i.e diff b/n existing file data and currently modified file data.
	     commit id/check in :- with 40 char long
        in workspace we've 3 stages before commit id get generated
	        --> working dir:- where you working with files physically
	        --> Staging Area:- it helps to create commit id(it is virtual area , here workspace don't know which one is existing and modified data)
	        --> Repository:- where stores data (commited file)
git config:-
=========
git config --global user.name "VmTutes"
git config --global user.email "Vinodh-Machireddy@VmTutes.com

git config --global push.default simple
git config --global core.editor 'vi' 
git config --list

local  : By default, git config will write to a local level, if no configuration option is passed. .git/config
global : Global level configuration is user-specific, means it is applied to an operating system user. 
         Global configuration values are stored in C:\Users\vinodh\.gitconfig
		Ex:- One of the most common use cases for git config is configuring which editor Git should use. 
		     editor = VIM
		Ex:- Merging Tools 
		     git config --global merge.tool kdiff3
system : System-level configuration is applied across an entire machine. This covers all users on an operating system and all repos.
	 system configuration values are stored in C:\Program Files\Git\mingw64\etc\gitconfig

git config --edit/--list --local
git config --edit --global
git config --edit --system


creating Repositorys:-
1. bare repo: is the centrailized repository which is used to store and share the changes, but we cannot view the data.
2. non-bare repo: user (or) workspace (or) local repository whih is used to modify the changes.

mkdir central.git
git init --bare
git clone central.git <source>  vinuspace <dest>
create file in workspace 
move to staging area : git add java
move from staging repo : git commit -m "first chickin"

-->git log : list of all the commits will display
--> set of changes together with single version id: git add . (or) java, oracle...etc

if you don't have the same content then-->Modified/Untracked files
if you have same content in the file then --> Unmodified 

--> git push <source> <dest>
--> git push enter : to push the changes to repository for sharing to other users
--> 2nd user access the repo and created new file and pushed it to central repo and now
     1user want to update things what user2 changed. then use
-->git pull

Git ignoring:
=============
--> .gitignore : is a conf file to ignore the unwanted runtime files like jar, war, log....
              1.class (Full name)
             *.class (pattern matching)
	      
Log viewing:
============
--> git log -3
--> git log --oneline --grep "workspace"
--> git log --pretty=oneline
--> git log --grep "stringmasg" --oneline
--> git shortlog
--> git log --stat
git show --stat 23rt459bf
git show --name-status 23rt45bf
git show --name-only abc
git log hello.txt

Branching:- 
===========
--> parallel development
--> storing of files in a repo is in the form of branches 
       ex:  android 			windows
               file1			    file1
               file2			    file2
              	
       here the futures are same only slight diff i.e os
--> master is the default branch whenever we create repository/workspace
--> at any point of time you can work with  only one branch at a time
--> git branch : list of branches avilable
      git branch branch_name
      git checkout new_branch : switch to other branch
      git checkout -b new_branch_name : creating new and switching to new branch
--> when we create a new branch based on the master the same fiels and commit ids will come to new branch also.
# merging the 2 branches:-
--> git merge <sour> <dest>
--> git branch -d <branch_name> : to delete branch, use 'D' for forcely remove without fully merged.
--> git branch --merged:- lists the branches that have been merged into the current branch
--> git branch ñno-merged:- lists the branches that have not been merged
--> git rebase :Alternate to merge 

Note:- when we create,edit,delete in workspace, this shows same in all branches until you commit permanently. 
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>


--> bare repo  you will not have working dir, so i.e you not able to see

Merging:-
=========
--> Master(Target)<---------feature(source)  

cherry-pick
===========
it picks the specific commit-id for merging. 
eg:-  git cherry-pick a620252dbebc44a63ef8fc3041b5eef82d3089ef

checkout command:-
==================
1. git checkout <BRANCH>:<COMMITID> --> specific commit('detached HEAD')
2. git checkout branch_name --> to switch one branch to another  
3. git checkout -b <new-branch-name> --> creating and directly switching to new branch 
4. git checkout -- file1 file2 --> to dicard the changes in working directory(when only files deleted,edited from work dir)

Stash::
=======
saving(backup) your un-commited changes and also you can get it back(restore) whenever you want.
git stash save "message" --> it will do 2 things 
	1. whenever you modifing the changes it will take backup.
	2. and it revert back with orginal position of the file where you started. 
git stash list  --> list all stashes
git stash apply stash@{0} --> to apply(restore) the changes
git stash pop   --> it will apply and remove the last stash array[0]
git stash drop  --> it will drop the latest one (or) you can specify perticular one also eg:- git stash drop stash@{3}
git stash clear --> remove all backup stashes.
git stash show  --> it shows the changes that are there in the stash 

file types in git repositories

    tracked file -->  a file which has been already staged/indexed and committed.
       * git stash
    untracked file --> a file which has not been already staged or committed.
       * git stash -u save "message"
    ignored file --> a file which Git has been explicitly told to ignore. (eg:- .gitignore)
       * git stash -a  save "message"

Removing files:
===============
rm
git rm filename 
git clean -n(dry run means which are the file eligible to remove, very care full before running this)
note: removes untracked files
git clean -f( removes the untracked file instead of adding to .gitignore conf file)

Removing files in working Dir:-
===============================

git rm :- will remove the file from the index and working directory ( only index if you used --cached ) -
so that the deletion is staged for next commit.
When using git rm, the removal will part of your next commit. So if you want to push the change you should use git rm
rm:-However, if you do end up using rm instead of git rm. You can skip the git add and directly commit the changes using: git commit -a


Undo's     
=====
i added a file into staging area, now i want to modify it before going to commit it?

	      1. git reset (mixed is the default option) 
              2. git reset --hard --> to remove changes from all the 3 areas
						@ working directory
						@ staging Area
						@ Repository(once file/action arrives to staging area, it creats temperary commit id in commiting area)
             
               3. git reset --soft --> It only removes temp/ref id from commiting/git directory

Undo/Reverting Changes after commiting:-
=======================================
   1. git revert 256ed01(1st 7char)  --> it revert only the content not the complete entry(commit id)  and create a new commit id and refering to previous.
 
HEAD:-
======
HEAD is the reference to the most recent commit in the current branch(In most of  the cases).
HEAD Doesn't point to most recent commit when we go into DETACHED HEAD State. 
  git show HEAD --> to see head commit
  git difftool HEAD HEAD~1

Snapshot
=========
 it store difference between the files in the form of snapshort

    WD		  STG
 VmTutes   VmTutes
 ----------   -----------
  line1          line1
  line2          line2
  line3          line3 (snapshort)

Tags/labels:-
------------
to identify/reference for a commitid to quick access/ creating specific point in history for our repository

create tag for particular commits:
git tag <tag-name> <reference of commit>

git tag <name-of-tag> --> light weight tag
git tag -a <tag-name> -m "comment" <commitid> --> annotated tag
git tag -n9 --> to see tag messgaes
git tag --> to list tags
git show --stat <tag_name>
git push origin v7.2 ---> pushing to remote(github)
git push origin --tags ---> pushing all tags at once to remote
git push --tags
Note:- when you working in folder in which github repository is cloned)

Deleting tags from local repository:
git tag -d <tag_name>
git tag -delete <tag-name>
git tag -d v7.2 vinumaa v7.3 --> deleting multiple tags at once in local repository

Deleting tags from remote repository:
git push origin -d v7.2
git push origin -delete v7.2
git push origin :v7.2
git push origin -d v7.2 vinumaa v7.3 --> deleting multiple tags at once in remote repositor

we cannot checkout tags in git but, we can create a branch from tag and checkout the branch
git checkout -b <branch_name> <tag_name>(give already created tag names)

Diff:-
======
used to compare Changes,branches,and commits.
git diff --> diff b/n version in the working dir and version in the staging/index area 
git diff HEAD --> diff b/n version in working dir and commiting dir
git diff --cached --> diff b/n staging and commit versions
git diff --name-only
git diff --stat 
git diff master..VmTutes(current branch is optional)
git diff master..VmTutes --name-only
git log master...VmTutes  (Note: git diff requires triple dot .. and git log requires double dot ... to get the exact behaviour.) 

Rewriting Commit Messages/History:-
=================================
--> git commit --amend -m "new message"  (rewriting the commit message for latest commit)
--> git rebase -i(interactive) HEAD~2 : for other commits
note: use reword option, while r=editing commit message
--> git ls-files : for latet commit in current branch to list all files
--> git show --name-only <commit id> : specific file to list
--> git commit --amend --no-edit : # Edit hello.py and main.py git add hello.py git commit
				   # Realize you forgot to add the changes from main.py git add main.py git commit --amend --no-edit

 p, pick = use commit
 r, reword = use commit, but edit the commit message
 e, edit = use commit, but stop for amending
 s, squash = use commit, but meld into previous commit
 f, fixup = like "squash", but discard this commit's log message
 d, Drop = remove commit

rebase --continue
rebase --abort
rebase --skip

Fetch and pull:-
----------------
pull = fetch + merge
git fetch origin: i.e all the repos in the github will come to local repository,
git merge origin/master : to integrate the commitids 

workflow:-
=========
	     |		Add	       |	Commit	       |			      |	 	
	     |------------------------>|---------------------->| 			      |  		       			      
	     |----------------Commit -a ---------------------->|	  git push            |
	     |			       |		       |----------------------------->|
	Working Dir		     Index		Commiting Area 		      Remote Repository(GitHub)
	(work space)  	  	   (Staging)	    	    (HEAD)			      | 	
	     |			       |		       |<----------git fetch----------|
	     |<-------------------Merge------------------------|			      |	
	     |			       |		       |			      |	
	     |<----------------------------------Pull-----------------------------------------|
	     |<--------------------diff HEAD------------------>|			      |
	     |<----------diff--------->|	


Note:- the above commit -a option will only work for already known files to staging area(i.e old files)	
	   	    
reflog:-
========
it shows when we commit,checkout branch, reset....etc
git reflog 
git reflog show --all
git reflog show <branch_name>
git reflog master@{1.minute.ago}
git reflog show HEAD@{5}

** Basically "git blame <file_name>" is used to show what revision and author last modified each line of a file. 
   It's like checking the history of the development of a file.

                                                    ====THE END====       
			VmTutes, +91-7204143230(WhatsApp/Call), Email:- Vinodh-Machireddy@VmTutes.com







Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>








