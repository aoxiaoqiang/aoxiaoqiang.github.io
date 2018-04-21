# 工具推荐

## SSH

[SSH 官网](https://www.ssh.com/ssh/command/)

SSH 公钥默认储存在账户的主目录下的 ~/.ssh 目录。可进入`~/.ssh` 目录查看是否存在\*.pub 文件

```sh
# 生成公钥
ssh-keygen

# 上传公钥文件至服务器
ssh-copy-id -i ~/.ssh/tatu-key-ecdsa user@host

# 实用ssh登录
ssh -p port user@host
```

## Git

[官方文档](https://git-scm.com/book/zh/v2)

![git命令速查表](../assets/image/git.png)

### 常用命令

```sh
git add .
git commit -m 'commit message'
git push [remote name] [branch name]
git pull [remote name] [branch name]
git fetch [remote name] [branch name]
git log

#【git设置和取消代理】

git config --global https.proxy http://127.0.0.1:1087
git config --global https.proxy https://127.0.0.1:1087
git config --global --unset http.proxy
git config --global --unset https.proxy

npm config delete proxy

#【仓库关联操作】
添加: git remote add origin [url]
修改: git remote set-url origin [url]
删除: git remote rm origin

#【分支操作】
git branch -D [branch name] #删除本地分支
git push origin :[branch name]  # 删除远程分支(注意 origin 后面有空格)
```

### git-ssh 配置和使用, [GitHub with SSH][github-with-ssh]

* git 账号配置

```sh
git config --global user.name "aoxiaoqiang"
git config --global user.email "aoxiaoqiang@163.com"
```

* 生成密钥(连续 3 个回车。如果不需要密码的话。最后得到了两个文件：id_rsa 和 id_rsa.pub)

```sh
ssh-keygen -t rsa -C "aoxiaoqiang@163.com"
```

* 把公钥 id_rsa.pub 文件里的内容放到相应的站点(如: github.com gitlab.com conding.net 等)，然后测试是否配置成功。

```sh
cat ~/.ssh/id_rsa.pub   # 查看公钥内容
ssh -T git@github.com   # 这里测试的是 github.com站点是否添加ssh
```

### git提交检查 or 工具

* [git cz-cli][git-cz]

![cz-cli](https://github.com/commitizen/cz-cli/raw/master/meta/screenshots/add-commit.png)

* [gitmoji-cli][gitmoji-cli]

![gitmoji-cli](https://cloud.githubusercontent.com/assets/7629661/20454643/11eb9e40-ae47-11e6-90db-a1ad8a87b495.gif)

## AnyProxy

[AnyProxy github](https://github.com/alibaba/anyproxy)

[github-with-ssh]: https://help.github.com/articles/connecting-to-github-with-ssh/
[git-cz]: https://github.com/commitizen/cz-cli
[gitmoji-cli]: https://github.com/carloscuesta/gitmoji-cli
