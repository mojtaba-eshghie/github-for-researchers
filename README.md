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



## Git tags
Tags are just a feature to mark some point in repository. They are just labels that we can put at any arbitrary commit point. By default if we don't specify commit, they will be HEAD!

Using light tags:

    git tag mytag # will tag head
    git tag --list
    git hist # will also show tags
    
    # to delete tags:
    git tag -d mytag

Using anotated tags (which support adding more info):

    git tag -a v1.0 -m "Release 1.0"
    git tag --list
    git hist

The real use of annotated tags is when we `git show tagname`. It will show tagger, date, and the commit message we put on that tag, and after those the information of the commit that is associated with that tag:

    git tag -a v1.0.1 -m "Patch 1.0.1"
    git show v1.0.1

The result would b
![alt text](https://raw.githubusercontent.com/mojtaba-eshghie/github-for-researchers/master/resources/a_tags.png)



## Git stashing
Stashing can help us to save our in progress work in a stack like structure and retrieve it sometime else. If we think of the branch as a tunnel we are moving through, stashing is like a hole dug into the ground we can use to put our stuff (unstaged changes) in it to retrieve (pop) and stage & commit at some later time. 

    # first make some changes to a file like README.md, then:
    git stash 

    # now let's do some other changes other things, then stage and commit them.
    
    # now list the stashes we have
    git stash list 

    # as we said it may be used as an stack
    git stash pop 

    # now it is possible to stage and commit the changes 
    git add .
    git commit -m "changed the README.md file"

Alternatively it is possible to use `git stash apply` instead of `git stash pop`. If we want to use these stashes (stage and commit them) at different locations in our work.

A better approach would be to annotate your stashes:

    git stash save "Changed the last pragraph of readme file"

Using the stash id we can apply the ones that we want out of stack order:

    # for stash id 2 (id is written in front of each stash like stash@{2}:)
    git stash apply 2

