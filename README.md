# StartingOffWithGit-Github
Documenting git and github setup

---
Usefull Links:
---

[To determine what licence to use for your code](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)

---
Software needed:
--
Git needs to be installed and ready (I am using Gitbash with windows)

---
Command Line Basics
---
- You can use "cd" with just the name of the file to move into this directory or use "cd .." to move to previous directory. 
- Use "dir" to see the files in the directory if you need to. Alternatively, use "ls -la" to see the file names of all files along with their permissions and including hidden files starting with a period. 
- Press "CNTRL Z" to stop process. 
---
Initial Setup
---
To set up a project with git, we need to first initialize configuration variables to get credit for changes. 

Within Git, 

> git config --global user.name "Akash Patel"
> 
> git config --global user.email "email@email.com"

To check if it showed up, type in 
> $git config --global --list 

//--list will show changes local to settings so add --global to see exactly whats in .gitconfig

Make sure to use Github associated email address. Change email if necessary for different projects. 

Next, create a folder on your PC to store project files. Navigate to this directory in Git by using 

> cd c:/users/andthenwhereveritslocated

Next, use "git init" to manage projects in the folder of the directory you are in. Git will now store information about the project here. (if making repo local to computer only, not on github)

To make SSH key:
> Make sure .ssh folder exists in home dir. In .ssh folder, type in ssh-keygen in terminal. Find id_rsa.pub and open it in notepad. Copy public key from notepad and paste into github --> settings --> SSh Keys

or to clone someone else's or my stuff on github, make sure gitbash in correct directory where you want to clone and then do:
> git clone git@github.com:name/project.git
^SSH

-----
Staging Environment is a temporary area to store files we may want to commit later on. 
To move a file to staging, 
> git add FILENAME 

add * means add all files in the current directory, except for files whose name begin with a dot. This is your shell functionality and Git only ever receives a list of files.

add . has no special meaning in your shell, and thus Git adds the entire directory recursively, which is almost the same, but including files whose names begin with a dot.

Alternatively, can add all files using one of the following
> git add --all
> git add -A

Or, you can refer to current directory using the following
> git add .

To finally commit, use
> git commit -m "First Commit"

To see what git has kept track of so far, use "git log" 

"git status" lets you see what changed in your clone's current branch before commiting. 

HEAD indicates the current commit you are viewing

---
Git environments and File States
---
Git environments
- Working: updated to last commit
- Staging: temporary location to queue changes (add) 
- Commit:  creates new log entry with new hash (commit)

File States
- Tracked:   All commits
  -  Unmodified: files havent changed since last commit
  -  modified:   files have been changed
  -  Staged:     at staging environment
- Untracked: new files not commited yet

When a file is not staged for commit, can discard changes with "restore" or move to staging with (add)
> git restore FILENAME

To restore current directory
> git restore .

Older version of restore 
> git checkout .

---
Ignoring files to avoid sharing info on github
---
Create .gitignore file with "touch .gitignore" or manually in file explorer

Add what you want to ignore inside this file. ex: ".vscode/", "notes/"

You can also use a global ignore file:
> git config --global core.excludesfile [file]

Clear cache when adding new conditions to .gitignore
> git rm -r --cached .

Then add and commit again 

---
Deleting files
---
To delete a file AND move this to staging, 
> git rm FILENAME

To undo this, restore the file from staging, then restore the file to discard changes
> git restore -S .
>
> git restore .

---
Renaming Files
---
If done manually, shows deletion of original name and creation of new name as we are essentially creating new file and deleting the old one

mv is used to move files. This works by moving the file to a new name and deleting the old one as mentioned above. 

Rename file with the following
> git mv OLDFILENAME NEWFILENAME
---
Make Tag in GitBash
> $ git tag NameofTag_version

Send to Github
> $ git push --tags

Delete Tag
> $ git tag -d NameOfTag


---
Comparing Differences between branches
---
> git diff

---
vim: built in text editor
---

---
put & at end: Opening File or executing .exe w/out occupying terminal
ex. notepad fileName.md &
//include process id
---

Other Useful Commands
---
- git push :  Updates github with new code changes from your clone (from git to github) - own branch
- git pull :  Updates clone with new code changes from github (from github to git) - own branch
- git fetch: Updates clone with new branches (from github to git) - clone knows about other branches
- git merge [branch_name]: Combines code from any branch and your current branch (in git or github)
  - harder to fix merge conflicts on github
- git merge --abort: undo merge if there are merge conflicts (can use to redo resolving merge)

- git clone [github repo url]:     create a local clone of the github repo in your local computer
- git remote -v:                   this will tell you what .git servers (or mirrors) your clone is using. The origin one is what your clone was created from
- git add [file_name(s)]:          adds new files to track in current git branch
- git add -u [file_name(s)]:       updates tracked files to be committed in current git branch
- git checkout [file_name(s)]:     undo all changes from the specified file
- git commit -m "[commit message]": create a commit for your current branch with a commit message (each commit has a unique commit id)
- git checkout -b [branch_name]:   create a new branch based on the current branch you are on
- git checkout -t [branch_name]:   change to a new branch you haven't been on before in your local clone (only need to do this first time only)
- git checkout [branch_name]:      switch to a branch that is already existing on your local clone
- git checkout [commit_id]:        switch to an older version of your current branch based on your commit history from git log
- git checkout HEAD:               go back to your current version of your branch
- git reset HEAD:                  undo a git add if you accidentally add files or changes you do not want to commit
//ex. git HEAD~2: resets to 2 commits prior to current head (unstaged)
- git revert [commit id]:          undo a commit that was made in your current branch
- git stash:                       save off changes without adding or commiting on your local clone before switching to a new branch (for code you're not ready to commit)
- git stash pop:                   recover and get back the saved off changes in the branch you ran the git stash command on

you can configure the .gitconfig files for setting up various things like username, email, difftool, mergetool, and many other configurations.
you can update the .gitignore file to ignore specific files for version control such as binaries like .exe files.

The following are for ONLY if you're working with multiple git servers. You may have clones that update multiple github repositoriies. Or this may be useful if you have a PC that can access your computer (which has github access) but not have access to github or the internet. For example, a virtual machine or something similar.

- git remote add [remote variable] [git server url]: this is for if your clone is using multiple servers. You can have one clone update multiple github repositories.
- git clone --mirror [github repo url]: creates a server that you can put on a machine if another PC cannot access github. this is a .git folder which can act as a git server
- git push [remote varaible] [branch name]: push your changes to the specific git server you're interested on updating
- git pull [remote variable] [branch name]: pull your changes from from a specific git server

Can have single clone push or pull from multiple git servers like github
and gitlab
- git remote add gitlab git@gitlab.com:group14301423/Project1.git
- git remote -v //check all remote git server's that clone is using
//will need to specify after
- git remote -v //remove server

- git branch -a //Show remote vs local branches
- git branch //shows only local branch
- git branch -r //show only remote branches

Can create own git server (git mirror)

git diff options
- git diff
- gitk > meld
- git diff tool > meld
- meld (free)
- beyond compare (cost $$$)

GOOD PRACTICE
- Commit message: 
branchName: commit message

update message
- git rebase -i HEAD~2 //2 signifies latest at bottom to oldest at top
- squash or s merges commit to 1 before (merges to oldest)
