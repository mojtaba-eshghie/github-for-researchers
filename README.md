### To see a history of the commits:
    git log
    git log --oneline --graph --decorate --all
*The --decorate will show which commit belongs to which branch*

#### Creating a git history command (using git aliases): 
    git config --global alias.hist "log --oneline --graph --decorate --all"
*We use --global so that we can use this alias at user level not at this repository level. Now let's pass additional parameters to our alias: (returning only the history of LICENSE.md file)*
    git hist -- LICENSE.md

#### Looking at list of git's config entries:
    git config --global --list


### Unstaging from git (modifications to the README.md file will not be lost, rather it is just the file being unstaged from git staging area):
    git reset HEAD README.md 

### To get back to the the last unstaged modified file (the known good state of that file):
    git checkout -- README.md


### File operations with git:
*If I just 'mv' a file (with the intention of renaming it) inside the git repostory, then the new file will not be staged (if the former has had been already), thus, we try to  use the git's ecosystem and command:* 

    git mv example.txt demo.txt

*And now if we 'git stat's, it will show us that the demo.txt has the same status as the former example.txt. Do not forget to commit!*

#### File removal in git:
    git rm demo.txt 



<br>
<br>

### git configs

#### saving credentials

    git config credential.helper store



## Dealing with conflicts
Let's say we have two branches like so:

    git checkout -b secondary

That branch plus the master branch, and now let's assume we are editting in both branches and creating conflicts:
    
    git nano the_file.txt #already in secondary branch
    git add . 
    git commit -am "this is a bad commit"
    git checkout master
    git nano the_file.txt #changing to smt else
    git add . 
    git commit -am "this one is a bad commit as well"
    git merge secondary # merging master with secondary

As you can guess, the last command will raise an error. You can use mergetool (if you have already configured in ~/.gitconfig file). The best tool is p4merge.

    git mergetool

In the bottom of the application you can decide if the proposed final file is good or not, then save it, and close the mergetool. 
