# node安全局安装模块任然报错找不到命令问题

最近在做一个koa写后端的一个小项目，项目发到服务器上后想在服务器端使用Node中[apidoc](http://apidocjs.com/)模块在服务器端运行，生成接口文档。然而在服务器端运行 `npm install apidoc -g` 之后，使用 `apidoc -i myapp/ -o apidoc/` 结果报错，提示命令不存在，尝试了两次都失败了。


![](https://user-gold-cdn.xitu.io/2019/2/1/168a4db6a7712d98?w=838&h=518&f=png&s=77072)


后来搜了一些资料发现，应该是环境变量问题，设置环境变量应该就可以了。

具体步骤:

1. 通过`npm config get prefix`查看目前`npm`的默认路径；

```shell
➜ npm config get prefix
/usr/local
```

这里可以看到默认的路径级别很高，有些用户可能没有办法访问到，然后就会出现安装完成无法使用的情况。
所以我们要创建一个让当前账号能访问到的指定的路径，改变`npm`的路径；

2. 新建npm全局目录
```shell
# 在当前用户的根目录下创建
mkdir ~/.npm-global

# 将创建的目录设置为新的npm路径
npm config set prefix '~/.npm-global'
```

3. 至此已经创建完毕，要让系统能访问到就需要将`npm`地址设置为环境变量。
```shell
# 设置环境变量
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bash_profile

# 使配置改动生效
source  ~/.bash_profile
```
这里设置的是 `~/.bash_profile`, 我开始尝试设置后然后有问题题，后来发现我用的脚本不是`bash`,而是后来装的`zsh`。所以这理就直接设置`~/.zshrc` 就可以了。
```shell
# 设置环境变量
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc

# 使配置改动生效
source  ~/.zshrc
```


修改完成之后，检查一下 `npm config get prefix` 就是我们刚才新设置的 `~/.npm-global`, `~/.bash_profile`或者`~/.zshrc`中也有了我们新添加的环境变量。

再次尝试`npm i apidoc`, `apidoc -i myapp/ -o apidoc/` 就能正常运行了。




参考文章:
+ [Node.js生产环境配置](https://yq.aliyun.com/articles/462733)
+ [npm成功安装命令后,执行时却报找不到命令](https://blog.csdn.net/wirelessqa/article/details/53393248)