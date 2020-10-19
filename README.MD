# Git Commit Message Hook Example
date: 2020-10-19
author: Markus Wals, es19m012

## TODO 
Validate commit messages on all branches with a simple regex

## Solution
to enforce that commit messages start with PJM- followed by a 4 digit number.

How does this regex work?

```
^             Beginning of the string (line anchor)
PJM-          The Letters PJM followed by a - symbol
[0-9]{4}      Issue ID, 4 Digits that can be numbers from 0 - 9
\b            Word boundry
```

## Examples for good commit messages
PJM-0001 Anytext
PJM-9999 Some other text

## Script to set this up
```
mkdir commit-msg-hook

cd commit-msg-hook

git init

cd ./.git/hooks
cp commit-msg.sample commit-msg
rm commit-msg.sample#
nano commit-msg
chmod +x commit-msg
cd ../..

nano README.MD
git add README.MD
git commit -m "test"
	Your commit message does not match the specified pattern: PJM-<4 Digit Issue ID> <Commit Message>

git commit -m "PJM-0001 Initial commit on master"
	[master 3353091] PJM-0001 Initial commit on master
	 1 file changed, 2 insertions(+)

cp .git/hooks/commit-msg commit-msg
git commit -m "PJM-0002 Add commit-msg script"
	[master e376dff] PJM-0002 Add commit-msg script
	 1 file changed, 26 insertions(+)
	 create mode 100755 commit-msg

git checkout -b  develop
touch .develop
git add .develop
git commit -m "PJM-0003 Initial commit on develop"
	[develop 6387599] PJM-0003 Initial commit on develop
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 .develop

git checkout -b  release
touch .release
git add .release 
git commit -m "PJM-0003 Initial commit on develop"
	[develop 6387599] PJM-0003 Initial commit on develop
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 .develop

git checkout -b feature/PJM-0001
touch .feature_PJM-0001
git add .feature_PJM-0001
git commit -m "PJM-0004 first commmit on feature branch"
	[feature/PJM-0001 4c83ce9] PJM-0004 first commmit on feature branch
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 .feature_PJM-0001
touch .feature_PJM-0002
git add .feature_PJM-0002
git commit -m "PJM-0005 second commmit on feature branch"
	[feature/PJM-0001 cab94b6] PJM-0005 second commmit on feature branch
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 .feature_PJM-0002
touch .feature_PJM-0003
git add .feature_PJM-0003
git commit -m "PJM-0006 third commmit on feature branch"
	[feature/PJM-0001 affd0c1] PJM-0006 third commmit on feature branch
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 .feature_PJM-0003

git branch -l
	  develop
	* feature/PJM-0001
	  master
	  release

git remote add origin https://github.com/MWals/commit-msg-hook.git
git push -u origin master
```
