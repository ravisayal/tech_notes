# How to create copy of enterprise repo to a personal repo

This will be done by swapping the remote url of the repo 
1. sync up the local git folder with the remote master branch of Repo A
2. change the remote  url to Repo B
3. git push to Repo B - this will push the master branch to Repo B
4. change the remote  url back to Repo A
5. swtich the branch to child branch
6. Repeat step 1..4


> command line 

```unix
ras8804@UISWHLPT1000869 MINGW64 /c/01_harvard_git/test/test_rep (master)
$ git remote set-url origin https://github.huit.harvard.edu/ras8804/test_rep.git

ras8804@UISWHLPT1000869 MINGW64 /c/01_harvard_git/test/test_rep (master)
$ git pull

ras8804@UISWHLPT1000869 MINGW64 /c/01_harvard_git/test/test_rep (master)
$ git remote set-url origin https://github.com/ravisayal/test_rep.git

ras8804@UISWHLPT1000869 MINGW64 /c/01_harvard_git/test
$ git push

ras8804@UISWHLPT1000869 MINGW64 /c/01_harvard_git/test/test_rep (master)
$ git remote set-url origin https://github.huit.harvard.edu/ras8804/test_rep.git

ras8804@UISWHLPT1000869 MINGW64 /c/01_harvard_git/test/test_rep (master)
$ git checkout Child1
$ git pull 

$ git remote set-url origin https://github.com/ravisayal/test_rep.git

ras8804@UISWHLPT1000869 MINGW64 /c/01_harvard_git/test/test_rep (master)
$ git push
```
