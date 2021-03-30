

## Cheatsheet
https://git-scm.com/docs 
https://ndpsoftware.com/git-cheatsheet.html#loc=local_repo;
https://training.github.com/downloads/github-git-cheat-sheet/
https://training.github.com/downloads/github-git-cheat-sheet.pdf

git init 
git status

git add test.txt
git status

git commit

```
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.
```
## .git/config
git config user.email "you@example.com"
git config user.name "Your Name"

git config --unset user.email
git config --unset user.name

## ~/.gitconfig
git config --global user.email "ev45ive@gmail.com"
git config --global user.name "Mateusz Kulesza"

## VIM
https://stackoverflow.blog/2017/05/23/stack-overflow-helping-one-million-developers-exit-vim/
https://stackoverflow.com/questions/11828270/how-do-i-exit-the-vim-editor

cd projekt/
git add test.txt
git commit

## VIM
a - append -- WPROWADZANIE --
ESC - exit appen mode
:q - quit
:q! - quit and discard changes
:w - write
:q - quit
:wq - write & quit

## Pierwszy commit
[master (root-commit) 3273984] Mój pierwszy commit w VIM
1 file changed, 1 insertion(+)
create mode 100644 test.txt

## Poczekalnia
git log 
// zmiana pliku
git add .
git status
git diff
// zmiana pliku
git diff <idcommita> plik.txt


[   ] Working tree
  |
[   ] Staging ( poczekalnia / index )
  |
[   ] Last commit
  |
[   ] Last commit parent
  |
.....
git add log.temp.log
rm log.temp.log
git restore log.temp.log
rm log.temp.log
git add log.temp.log // add "remove" operation to index

```
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   log.temp.log
        modified:   test.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    log.temp.log
```

## Add all MODIFIED files and commit and message

git commit -a // === git add . + git commit

git commit -a -m "Drugi commit - Text with bang!"

WONT ADD UNTRACKED FILES!!

## Browsing
git log 
git show <commitid> --format="fuller"
git show  --format="fuller"

## Amend message
git commit --amend 

- unpacks commit to index
- recommits to new commit, new ID, new Committer, new Commit date

## Amend files - no edit message
git add .
git commit --amend --no-edit 

## Moving / Removing
git rm plik.txt
git mv plik.txt katalog/nowanazwa.txt

# REfs
master --> 53c1c5ddb
HEAD  --> 53c1c5ddb

## LOG
q - to exit log pagination

git log 9ce21a9
git log master
git log HEAD
git log HEAD~1
git log HEAD~4

git log --oneline -2 HEAD~2

git log --format="short"
git log --format="fuller"
oneline, short, medium, full, fuller, reference, email, raw, format:<string>
git log --oneline

git log --oneline -2 --before="1 hour ago" --grep="bang"
git log --oneline -2 --before="1 hour ago" --after="2 hours ago"
git log --format="%h %s"

## Log file
git mv staranazwa nowykatalog/nowanwazwa
git log --follow [file]
git log HEAD -- test.txt
git log HEAD -- test.txt -L 0:1:test.txt

## Restore old version of file
- locate file
- choose version
- checkout

git checkout 6b65fa5e test.txt

git checkout 6b65fa5e // git switch 6b65fa5e

## Revert old commit change
git revert 9ce21a9
git revert 6b65fa5 8611ad9


## Git alias
git config alias.st status
git config alias.log1 "log --oneline --decorate --graph --all" 
git log1  --before="3hours ago"
git config --list

https://github.com/GitAlias/gitalias
https://github.com/jakubnabrdalik/gitkurwa 


## Porcelain - Plumbing - NIE RÓB TEGO W DOMU! - psujemy GIT
https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain

## SHA1 
https://pl.wikipedia.org/wiki/SHA-1
git hash-object test.txt
30d74d258442c7c65512eafab474568dd706c430

git hash-object test.txt -w
30d74d258442c7c65512eafab474568dd706c430

.git\objects\30\d74d258442c7c65512eafab474568dd706c430
.git\objects\f0\79749c42ffdcc5f52ed2d3a6f15b09307e975e

git cat-file -p 30d74d258442c7c65512eafab474568dd706c430
test

git cat-file -p f079
test1

git cat-file -p 30d74d258442c7c65512eafab474568dd706c430 > test.txt

### Index
git update-index --add --cacheinfo 100644 30d74d258442c7c65512eafab474568dd706c430 test.txt

git write-tree
095a057d4a651ec412d06b59e32e9b02871592d5
git cat-file -p 095a057d4a651ec412d06b59e32e9b02871592d5
100644 blob 30d74d258442c7c65512eafab474568dd706c430    test.txt

 git commit-tree -m "First commit" 095a057d4a651ec412d06b59e32e9b02871592d5
1e1c492d67e21751de608233f9d1e406c131be91

 git cat-file -p 1e1c492d67e21751de608233f9d1e406c131be91
tree 095a057d4a651ec412d06b59e32e9b02871592d5
author Mateusz Kulesza <ev45ive@gmail.com> 1617020117 +0200
committer Mateusz Kulesza <ev45ive@gmail.com> 1617020117 +0200

First commit

git branch master 1e1c492d67e21751de608233f9d1e406c131be91

git hash-object subdirectory/test2.txt
30d74d258442c7c65512eafab474568dd706c430

## subtree
git update-index --add --cacheinfo 100644 30d74d258442c7c65512eafab474568dd706c430 test2.txt

write-tree
df09887a12bbe162a9b4cf839c191d350b609010

git read-tree --prefix=subdirectory df09887a12bbe162a9b4cf839c191d350b609010
125c118d7e2bd1413d66b7e8c204059d4125c66f

git cat-file -p 125c118d7e2bd1413d66b7e8c204059d4125c66f
040000 tree df09887a12bbe162a9b4cf839c191d350b609010    subdirectory
100644 blob 30d74d258442c7c65512eafab474568dd706c430    test.txt
100644 blob 30d74d258442c7c65512eafab474568dd706c430    test2.txt

## second commit
git commit-tree -m "second commit, subdir" -p 1e1c492d67e21751de608233f9d1e406c131be91 125c118d7e2bd1413d66b7e8c204059d4125c66f

aff18946f054244449eb0e9f567eb9f620d6d77e

git cat-file -p aff18946f054244449eb0e9f567eb9f620d6d77e
tree 125c118d7e2bd1413d66b7e8c204059d4125c66f
parent 1e1c492d67e21751de608233f9d1e406c131be91
author Mateusz Kulesza <ev45ive@gmail.com> 1617021146 +0200
committer Mateusz Kulesza <ev45ive@gmail.com> 1617021146 +0200

second commit, subdir

git reset aff18946f054244449eb0e9f567eb9f620d6d77e

## Moving refs
git reset --hard <commitRef>

git reset --mixed <commitRef>
git reset --soft <commitRef>

## Rebase
git rebase -i 53c1c5d

```bash
reword 25cb344 Revert "Removed test.txt"
f 3759379 Revert "Trzeci commit - poprawki, triple bang!"
f e19ccbc Revert "Drugi commit - Text with bang!"
pick 54b43b3 Porcelain + Plumbing - puste katalogi
e 741638b Git Ignore
pick f7dbad9 Nagłowek i podstrony
label naglowek
pick 56d7122 Polecenia i notatki

# Rebase 53c1c5d..56d7122 onto 53c1c5d (7 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
```

## Add patch
 <nav>
     <ul>
       <li><a href="index.html">Strona głowna</a></li>   
+      <li><a href="strony/kontakt.html">Kontakt</a></li>
     </ul>
   </nav>
   
(1/2) Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]? ?
y - stage this hunk
n - do not stage this hunk
q - quit; do not stage this hunk or any of the remaining ones   
a - stage this hunk and all later hunks in the file
d - do not stage this hunk or any of the later hunks in the file
g - select a hunk to go to
/ - search for a hunk matching the given regex
j - leave this hunk undecided, see next undecided hunk
J - leave this hunk undecided, see next hunk
e - manually edit the current hunk
? - print help

## Pusty commit
git commit -m "Strona do opublikowania" --allow-empty

## Create branch
git branch nazwa_brancha <hash>

## delete
git branch -d nazwa_brancha

## Create branch
git checkout -b nazwa_brancha
git switch -c nazwa_brancha

# Switch to branch
git checkout nazwa_brancha
git switch nazwa_brancha

## work on branch
git commit ...
 

### Update branch with lastes master
// when master changed 

git switch nazwa_brancha

git merge master
// or
git rebase master

### merge branch into master
git merge master
git merge nazwa_brancha

## Fast-forwartd
git merge nazwa_brancha --only-ff
git merge nazwa_brancha --no-ff

## Chery pick one commit
git cherry-pick 90ede47 23w5g44 9q43240


## Excercise
- create WIP branch from master
- add page header, commit
- create WIP branch from master
- add page footer commit
- 

## Remote work
git fetch  
git pull  // git fetch + git merge FETCH_ORIGIN
git push
git clone
git remote
