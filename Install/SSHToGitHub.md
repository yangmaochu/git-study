# 配置GitHub仓库的密钥访问

## 第一步：生成密钥

```
mkdir ~/.ssh
chmod 700 ~/.ssh
ssh-keygen  -b 2048 -t rsa -C "yangmaochu@hotmail.com" -f ~/.ssh/ymc.rsa
chmod 600 ~/.ssh/ymc.rsa
```

脚本说明：

* `ymc.rsa`是自定义的私钥文件名,公钥文件自动命名为`ymc.rsa.pub`
* `yangmaochu@hotmail.com`是自定义的备注
* `chmod`命令赋予文件合适的权限

## 第二步：`.ssh/config`文件中增加到GitHub的SSH连接配置

```
Host	github
	HostName	github.com
	Port		22
	User		git
	IdentityFile    ~/.ssh/ymc.rsa
```

## 第三步：将公钥添加到github上

1. 复制key(~/.ssh/ymc.rsa.pub文件内容)到剪贴板
2. 登录github
3. 点击右上方的图标后，选择`settings`
4. 选择 SSH and GPG keys
5. 点击 New SSH key
6. Title随意填入，将key粘贴到输入框后点击Add SSH key。

# 访问GitHub

## 本地已经clone了自己的GitHub仓库

修改git项目根目录下配置文件`.git/config`

修改前

```
[remote "origin"]
    url = https://github.com/yangmaochu/git-study.git
    fetch = +refs/heads/*:refs/remotes/origin/*
```

修改后

```
[remote "origin"]
    url = ssh://git@github/yangmaochu/git-study.git
    fetch = +refs/heads/*:refs/remotes/origin/*
```

## 克隆自己在GitHub上的仓库

```
git clone -o git-study ssh://git@github:/yangmaochu/git-study.git
```
