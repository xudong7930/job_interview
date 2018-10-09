git 常用命令
=============

#create
git clone http://user@domain.tld/repo.git
git clone --recurse-submodules ssh://user@domain.tld/repo.git
git init

#config
git config user.name
git config user.email

#local changes
git status
git diff
git add 
git add .
git mv oldfile newfile
git rm oldfile
git commit -a #提交所有
git commit -m ""
git commit --amend "" #修改上次提交日志

#commit history
git log 
git log -p filename
git log --author="sbjsw@qq.com"
git log --grep=""
git blame filename #查看谁更改了指定的文件
git stash #临时保存文件的更改
git stash pop #弹出临时保存的更改
git rm --cached filename

#branch && tags
git branch 
git checkout branch.name
git branch -d branch.name #删除本地分支
git push origin --delete branch.name #删除远程分支

git branch -m oldname newname
git push origin/master :oldname
git push origin/master newname

git tag tag.name
git tag

#update & publish
git remote -v
git remote show
git remote show origin
git remote add remote.tagname url
git remote add origin url
git remote rename oldname newname

git fetch remote.tagname
git pull remote.tagname branch.name
git push remote.tagname branch.name
git push --tags

#merge & rebase
git merge branch.name
git rebase branch.name
git rebase branch.name --abort
git rebase --continue

git add resolved.files
git rm resolved.files


#undo
git reset --hard HEAD
git checkout HEAD file.name
git revert commit.name
git checkout commit.name file.name
git reset --hard commit.name
git reset commit.name
git reset --keep commit.name

#submodules
git submodule
git submodule status
