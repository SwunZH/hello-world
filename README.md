### My github training

#### following are the study memo of Pro git

VCS - Version Control System
RCS - Revision Control System
CVCS - Centralized Version Control System
DVCS - Distributed Version Control System (Git, Mercurial, Bazaar, Darcs)

Mechanism Gits use - SHA-1 hash

The Three States
Modified
Staged
Committed - safely stored in local database

### Chapter 2
## Git Basics
1. init/clone
2. Tracked/Untracked, staging, commit
Track: 
	git status
	/git status -s(short)
	git add
Staging (一定是已经tracked文件)
	git commit 无commit = not staged
ignoring files
git diff --staged/


3. Git log查看历史修改记录
doesn't show all the branches all the time
4. undo
	a. commit - git commit --amend
	b. unstaging a Staged file - git reset HEAD <file> 注: 2.23.0变成了restore
	c. revert - git checkout -- <files>
5. remote
查看所有remote内容 - git remote show <remote>
	a. fetch and pull
	fetch只是把其他branch拉下来不做merge
	pull自动fetch并且merge到current branch = fetch + merge
	b. push - git push <remote> <branch>
6. Tagging标记(eg mark release version)
Tag要单独push - git push origin <tagname>
		

### Chapter 3
## Branching - diverge from the main line of development and continue work without messing with that main line
他只记录commit和文件标签，然后通过一个head来指向当前branch内容(master 也是个branch)
1. 创建branch - git branch <branch name>
创建branch并切换 - git checkout -b <new branch name>
2. 切换branch - git checkout <branch name> 注: 2.23开始变成了switch
git switch test-branch
git switch -c new-branch (c = create)
git switch - (return)
3. 删除branch - git branch -d <branch name>
强行删除 - git branch -D <branch name> 
4. 查看branch - git branch
                 - git branch -v
5. 查看是否merge - git branch --merged/--no-merged
6. 更换branch名 - git branch --move <old name> <new name>
                             git push --set-upstream origin <new name>
                             git push origin --delete <old name>
7. rebase没搞懂…
		用于重写commit
	```
	git rebase --interactive 'xxxx&^'
	# pick, edit, reword…
	git rebase (--continue/--abort)
	
	#注意 一定要force push
	git push --force
	```


https://www.atlassian.com/git/tutorials/merging-vs-rebasing#:~:text=Merging%20is%20a%20safe%20option,onto%20the%20tip%20of%20master%20.

### Chapter 5
## Distrubuted workflows
如何控制多分支情况
Second developer must merge in the first one's work before pushing changes up.
5.1 给出不同解决方案，典型: push master的工作永远是一个人做的，其他分支branch的人不能擅自push/merge
5.2 git -add patch
      活用fork, 可以fork自己的代码给别人

### chapter 6 
## 实际运用
webhook

### Chapter 7 
## Git tools
stash = 不上传的commit
	git stash
	git stash apply
	git stash branch <new branch>
git clean - 删掉所有untracked 文件


### Chapter 8
git config设置
目前用法: 设置commit格式
查看git global config - git config --list --show-origin
设置commit default editor

visual studio code
```
git config --global core.editor "code --wait"
```
sublime text
```
git config --global core.editor "'C:/Program Files/Sublime Text 3/subl.exe' -w"
```
设置commit template
~/.gitmessage.txt中添加想要提醒自己commit的时候要写的内容
```
# Hint for commit
# 1. <title> 与 <description> 当中要空一行 	 Separate subject from body with a blank line
# 2. <title> 不超过 50 字，最多别超过 70 	 Limit the subject line to 50 characters
# 3. <title> 首词 首字 大写 				Capitalize the subject line
# 4. 不要用句号结尾 						 Do not end the subject line with a period
# 5. 命令式语气								Use the imperative mood in the subject line
# 6. <description> 不超过 72 字				Wrap the body at 72 characters
# 7. Use the body to explain what and why vs. how

```