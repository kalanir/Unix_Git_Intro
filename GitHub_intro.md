# Intro to GitHub

## Setting up GitHub on CL
```
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
```

## Setting up Github SSH key (Optional)
- https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
- https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account

## I want to create a new repository
Manually go onto your profile, click the + button at the top right, and click either import or create new repository. We generally have been adding the MIT license to our public repositories (cupcakes and coding).
example repo name: `GitUnix_Carpentries` (don't initialize ReadME)

## …and push my current repo up using the command line
example workflow:
```
echo "# GitUnix_Carpentries" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:kalanir/GitUnix_Carpentries.git
git push -u origin main
```

## I want to clone a repository and/or update
Cloning means: copying repository locally
- `git clone <https://github.com/username/example.git>`: you can find url on the repository you want to clone's home page. Click the green button that says "Clone or download" to do this
- `git pull origin master`: updates your local clone copy and deleting all the changes you made but didn't commit. perform this command while in your local clone folder. `git fetch origin`: is less aggressive and will update your file with updates remote changes, without deleting the ones you've made

## I want to make changes to a repository locally, and push them to my origin/master repository

- `git status`: will tell you if there are files/ file changes in your working directory that have not been committed to your repository
- `git add .`: start adding changes to the repository. You can add specific files but replacing . with the file. to undo this, `git reset` will undo changes
- `git status`: will tell you if changes have been staged - currently a git add does not make permanent changes
- `git commit -m "any message"`: commit these changes to your repository
- `git push`: commit to remote repository

example workflow:
```
➜  Unix_Git_Intro git:(main) git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   GitHub_intro.md

no changes added to commit (use "git add" and/or "git commit -a")
➜  Unix_Git_Intro git:(main) ✗ git add GitHub_intro.md
➜  Unix_Git_Intro git:(main) ✗ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   GitHub_intro.md

➜  Unix_Git_Intro git:(main) ✗ git commit -m "example push"
[main 089e25a] example push
 1 file changed, 1 insertion(+), 1 deletion(-)
➜  Unix_Git_Intro git:(main) git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 371 bytes | 371.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:kalanir/Unix_Git_Intro.git
   2c6c16a..089e25a  main -> main

```


## I want to make a branch off of a repository, and make changes, and push that branch
- `git checkout -b <branch name>`: creates a new branch and switches to that branch. you should be able to see a change in the path you are working in.
- `git status`: see if there are files to commit that are not on the branch
- `git add .` or `git add <file name>`: to start adding changes to branch
- `git commit -m "message"`: to commit changes to branch
- `git push origin <branch name>`: pushes branch to repository. Go online to decide whether to merge new branch to master if you have the permission to.
- `git checkout <branch name`: allows you to switch between branches

example workflow:
```
➜  Unix_Git_Intro git:(main) touch test.txt
➜  Unix_Git_Intro git:(main) ✗ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	test.txt

nothing added to commit but untracked files present (use "git add" to track)
➜  Unix_Git_Intro git:(main) ✗ git checkout -b 20210302_branch
Switched to a new branch '20210302_branch'
➜  Unix_Git_Intro git:(20210302_branch) ✗ git status
On branch 20210302_branch
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	test.txt

nothing added to commit but untracked files present (use "git add" to track)
➜  Unix_Git_Intro git:(20210302_branch) ✗ git add test.txt
➜  Unix_Git_Intro git:(20210302_branch) ✗ git status
On branch 20210302_branch
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   test.txt

➜  Unix_Git_Intro git:(20210302_branch) ✗ git commit -m "branch practice"
[20210302_branch 656d3e7] branch practice
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test.txt
➜  Unix_Git_Intro git:(20210302_branch) git push origin 20210302_branch
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 269 bytes | 269.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for '20210302_branch' on GitHub by visiting:
remote:      https://github.com/kalanir/Unix_Git_Intro/pull/new/20210302_branch
remote:
To github.com:kalanir/Unix_Git_Intro.git
 * [new branch]      20210302_branch -> 20210302_branch
➜  Unix_Git_Intro git:(20210302_branch) git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```
## I want to merge my branch to origin/master
- Go online and you will see a merge request
- Remember to git pull locally to get updates

## I want to revert file back to a previous commit
- `HEAD` vs `HEAD~1` vs `HEAD~123`: The most recent end of the chain is referred to as HEAD; we can refer to previous commits using the `~` notation, so `HEAD~1` means “the previous commit”, while `HEAD~123` goes back 123 commits from where we are now.
- `git diff HEAD~3 file.txt`: get differences between a commit (HEAD~3) and our working directory
- `git show HEAD~3 file.txt`: shows us what changes we made at an older commit (HEAD~3) as well as the commit message
- `git diff f22b25e3233b4645dabd0d81e651fe074bd8e73b file.txt`: get differences between working directory and particular commit id
- `git checkout f22b25e3233b4645dabd0d81e651fe074bd8e73b file.txt`: checks out (i.e., restores) an old version of a file by commit id
-  `git checkout`: put things back the way they were
- `git log`: displays commits using those long strings of digits and letters
example code:
```
➜  Unix_Git_Intro git:(main) ✗ echo "testing" >> test.txt
➜  Unix_Git_Intro git:(main) ✗ cat test.txt
testing
➜  Unix_Git_Intro git:(main) ✗ git add test.txt
➜  Unix_Git_Intro git:(main) ✗ git diff HEAD test.txt
➜  Unix_Git_Intro git:(main) ✗ git commit -m "test add"
➜  Unix_Git_Intro git:(main) ✗ echo "test2" >> test.txt
➜  Unix_Git_Intro git:(main) ✗ cat test.txt
testing
test2
➜  Unix_Git_Intro git:(main) ✗ git add test.txt
➜  Unix_Git_Intro git:(main) ✗ git commit -m "test5"
[main 571e556] test5
 1 file changed, 1 insertion(+)
➜  Unix_Git_Intro git:(main) ✗ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 257 bytes | 257.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:kalanir/Unix_Git_Intro.git
   9e88423..571e556  main -> main
➜  Unix_Git_Intro git:(main) ✗ git diff HEAD test.txt     
➜  Unix_Git_Intro git:(main) ✗ git diff HEAD~2 test.txt
➜  Unix_Git_Intro git:(main) ✗ git show HEAD~1 test.txt
➜  Unix_Git_Intro git:(main) ✗ git checkout b7d14460b25d25b03621e83e6dcd18b3d05367e4 test.txt
Updated 1 path from acf73bd
➜  Unix_Git_Intro git:(main) ✗ cat test.txt
➜  Unix_Git_Intro git:(main) ✗ git checkout HEAD test.txt
Updated 1 path from 98af8d8
➜  Unix_Git_Intro git:(main) ✗ cat test.txt
testing
test2
➜  Unix_Git_Intro git:(main) ✗ git checkout b7d14460b25d25b03621e83e6dcd18b3d05367e4 test.txt
➜  Unix_Git_Intro git:(main) ✗ cat test.txt
```
