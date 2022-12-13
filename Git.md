# Git

## SSH的问题

向 github 中配置好 SSH-Key 后仍然提示：
```
git@github.com: Permission denied (publickey).
致命错误：无法读取远程仓库。

请确认您有正确的访问权限并且仓库存在。
```

解决办法：

向系统添加生成的SSH私钥
```
ssh-add "私钥路径"
```
私钥路径通常为`/home/user/.ssh/filename`

**如果仍然出现上述错误，可能是电脑有多个ssh密玥？**
参考：https://zhuanlan.zhihu.com/p/281094708

编辑`~/.ssh/config`（如无则新建文件），添加以下内容：
```
Host github.com
	User git
	HostName github.com
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/github
	ServerAliveInterval 300
	ServerAliveCountMax 10

```