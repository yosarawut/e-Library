# Command line instructions

You can also upload existing files from your computer using the instructions below.

## Git global setup

git config --global user.name "yosarawut" git config --global user.email "yo\_sarawut@hotmail.com"

## Create a new repository

git clone git@gitlab.com:dragon\_e-Library/code-snippets.git cd code-snippets touch README.md git add README.md git commit -m "add README" git push -u origin master

## Push an existing folder

cd existing\_folder git init git remote add origin git@gitlab.com:dragon\_e-Library/code-snippets.git git add . git commit -m "Initial commit" git push -u origin master

## Push an existing Git repository

cd existing\_repo git remote rename origin old-origin git remote add origin git@gitlab.com:dragon\_e-Library/code-snippets.git git push -u origin --all git push -u origin --tags

> [Source : ](https://).

