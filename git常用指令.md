
# git本体操作

## git

~~~
git init \\初始化版本库（把目录变为版本库）
git add \\将工作区中文件提交到暂存区
git commit -m "remarks"\\将暂存区中文件提交到版本库，并在引号内写注释
git status \\查看本地库状态
git switch <branch> \\切换到<branch>
git push <remote respository> <local branch> \\将本地branch提交到远程库

git reset:
	git reset HEAD \\版本库重设为最新版本
	git reset HEAD^ \\版本库退回上一个版本
	git reset HEAD^^ \\~退回上上一个版本
	...
	git reset HEAD~n \\~退回第n个版本前的版本


~~~

## git branch

~~~
git branch -d <branch name> \\删除branch
git branch -D <branch name> \\强制删除branch
git branch <branch name> \\创建名为branch name的新分支
git branch \\查看分支列表
git cherry-pick <commit ID> \\将指定commit在当前分支上再执行一次
~~~

## git log

~~~
git log \\查看最近的commit记录（详细）（优先显示五条）
git reflog \\显示所有操作（？）
git log\reflog -v \\ 同上，默认详细显示
git log\reflog -pretty=oneline \\简洁显示记录（代码+备注）
git log -graph \\图形化显示git commit log
~~~
- 温馨提示：没显示完的log按住enter显示更多，按一下Q键退出（回到输入模式）

## git stash

~~~
git stash \\将当前工作区储藏起来
git stash list \\查看储藏列表
git stash apply stash@{n} \\将代号为n的储藏释放（不删除储藏）
git stash drop stash@{n} \\手动删除代号为n的储藏
git stash pop stash@{n} \\将代号为n的储藏释放（自动删除储藏）
~~~

# 其它操作（

## 创建并初始化git库

~~~
mkdir <fold name> \\创造目标路径
cd <fold name> \\进入目标文件夹
pwd \\显示当前目录
~~~

## 配置代理相关

- 代码主要来源于CSDN，用于解决 git push 失败的问题

### http代理&socks5代理

~~~
# 配置socks5代理
git config --global http.proxy socks5 <IP>
git config --global https.proxy socks5 <IP>

# 配置http代理
git config --global http.proxy <IP>
git config --global https.proxy <IP>

#查看代理
git config --global --get http.proxy
git config --global --get https.proxy

#取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy

~~~

### SSH代理

- 在C:\Users\USER NAME\.ssh中的config内加入
	~~~
	Host github.com *.github.com
	  User git
	  Port 22
	  IdentityFile "~\.ssh\id_rsa"
	  # SOCKS代理
	  ProxyCommand nc -v -x <ip> %h %p
	  # HTTPS代理
	  ProxyCommand socat - PROXY:<ip>:%h:%p,proxyport=<port>
	
	~~~

- 没有config就自己创建一个