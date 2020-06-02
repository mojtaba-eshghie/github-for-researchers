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