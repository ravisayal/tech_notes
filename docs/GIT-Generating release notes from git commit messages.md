# Generating release notes from git commit messages using basic shell commands (git/grep)

https://blogs.sap.com/2018/06/22/generating-release-notes-from-git-commit-messages-using-basic-shell-commands-gitgrep/


#### Showing commits since a given tag/version until now

` git log --pretty="%h - %s (%an)" 20.03.04..HEAD `

> Output
```
$ git log --pretty="%h - %s (%an)" 20.03.04..HEAD
46af808 - Code Changes for #223 (Ravinder Sayal)
9ddc805 - added changes for issues #214,#220. (#230) (Ravinder Sayal)
a74c793 - Code changes for #114 (#229) (Ravinder Sayal)
f255c75 - added change for issue #223 (Sachin Chauhan)
61da008 - added changes for issues #214,#220. (Sachin Chauhan)
d40144c - Added Notes field in the Lookup screen (#212) (Ravinder Sayal)
a2aacbd - 20.04.01 - Addendum-01 (Ravinder Sayal)
dbd18a8 - Release 20.04.01 (Ravinder Sayal)
d96541c - Changes to Print version of data collection script in TRUE Output Issue #210 (#211) (Ravinder Sayal)
e4fe935 - Remove hard coding of Compliance files #198 (#208) (Ravinder Sayal)
b7a128d - Code changes for #186 (#207) (Ravinder Sayal)
4cbeed4 - Seed Data scripts for #190 (#206) (Ravinder Sayal)
6442046 - Code changes for #129 (#203) (Ravinder Sayal)
59ee49e - Code changes for #179 (#199) (Ravinder Sayal)
```
