# node 全局安装模块任然报找不到命令问题

最近在做一个 koa 写后端的一个小项目，项目发到服务器上后想在服务器端使用 Node 中[apidoc](http://apidocjs.com/)模块在服务器端运行，生成接口文档。然而在服务器端运行 `npm install apidoc -g` 之后，使用 `apidoc -i myapp/ -o apidoc/` 结果报错，提示命令不存在，尝试了两次都失败了。

![error-image](https://user-gold-cdn.xitu.io/2019/2/1/168a4db6a7712d98?w=838&h=518&f=png&s=77072)

后来搜了一些资料发现，应该是环境变量问题，设置环境变量应该就可以了。

具体步骤:

1. 通过`npm config get prefix`查看目前`npm`的默认路径；

```shell
➜ npm config get prefix
/usr/local
```

这里可以看到默认的路径级别很高，有些用户可能没有办法访问到，然后就会出现安装完成无法使用的情况。
所以我们要创建一个让当前账号能访问到的指定的路径，改变`npm`的路径；

2. 新建 npm 全局目录

```shell
# 在当前用户的根目录下创建
➜ mkdir ~/.npm-global

# 将创建的目录设置为新的npm路径
➜ npm config set prefix '~/.npm-global'
```

3. 至此已经创建完毕，要让系统能访问到就需要将`npm`地址设置为环境变量。

```shell
# 设置环境变量
➜ echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bash_profile

# 使配置改动生效
➜ source  ~/.bash_profile
```

这里设置的是 `~/.bash_profile`, 我开始尝试设置后然后有问题，后来发现我用的脚本不是`bash`,而是后来装的`zsh`。所以这理就直接设置`~/.zshrc` 就可以了。

```shell
# 设置环境变量
➜ echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc

# 使配置改动生效
➜ source  ~/.zshrc
```

修改完成之后，检查一下 `npm config get prefix` 就是我们刚才新设置的 `~/.npm-global`, `~/.bash_profile`或者`~/.zshrc`中也有了我们新添加的环境变量。

再次尝试`npm i apidoc -g`, `apidoc -i myapp/ -o apidoc/` 就能正常运行了。

!> 至此问题是解决了, 后来有想起了另一个问题: 这里我们使用的`apidoc`是全局安装的，而普通项目里的依赖是在项目单独中安装这两个有什么区别呢? 什么原因导致全局安装成功后不能使用呢?

```shell
# 两者有什么区别
npm install apidoc
npm install apidoc -g
```

添加了`-g`顾名思义就是全局的意思，项目中的依赖安装是保存在项目文件夹下面的`node_modules`中，在使用时`require`的模块，会根据 Node.js 中的模块系统的模块加载顺序去查找, 最终会到当前目录下`node_modules`下面的模块文件。

![nodejs-require](http://www.runoob.com/wp-content/uploads/2014/03/nodejs-require.jpg)

由此推理，全局安装的模块是下载模块文件，区别是把文件放在系统中一个指定的目录下； 并且把当前的模块命令添加到系统的命令(当前模块的路径添加到全局 PATH 中)。这样在执行的时候，查找模块就会在系统中找到对应的模块。如果过程中因为权限之类的找不到相关模块肯定执行的时候就出问题了。

所以为了保证全局安装的模块正常使用，只要保证上的流程 OK 就行了:

1. 获取`npm config get prefix`返回的路径。需要用户要有权限访问，如果没有权限也可以自定义`npm`路径`npm config set prefix '~/.npm-global'`(我这里创建的是`~/.npm-global`目录);

```shell
➜ npm config get prefix
➜ mkdir -p ~/.npm-global
➜ npm config set prefix '~/.npm-global'

# 验证看是否设置正确
➜ npm config get prefix
```

2. 将`~/.npm-global`目录设置到全面`PATH`中，保证命令使用的时候能找到。 这里设置的时候得注意一下设置在哪个配置文件中，如果是用的是系统 shell 脚本，可以直接设置`~/.bash_profile`, 我使用的还是 zsh 这里就设置的是`~/.zshrc`; 然后让配置生效`source ~/.bash_profile` 或 `source ~/.zshrc`。

```shell
➜ echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bash_profile && source ~/.bash_profile

➜ echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc && source ~/.zshrc
```

设置完成后后, 全局安装的模块就会在`~/.npm-global/bin`文件下生成一个命令`link`, 指向到保存在系统中的全局模块。这样使用的时候就可以正常使用全局模块命令了。

参考文章:

- [Node.js 生产环境配置](https://yq.aliyun.com/articles/462733)
- [npm 成功安装命令后,执行时却报找不到命令](https://blog.csdn.net/wirelessqa/article/details/53393248)
- [nodejs 全局安装和本地安装的区别](http://www.cnblogs.com/PeunZhang/p/5629329.html)
- [npm install](https://www.cnblogs.com/chyingp/p/npm-install-difference-between-local-global.html)


<div id="gitalk-container"></div>
<script>
  var gitalk = new Gitalk({
  clientID: 'f4cf3934cb701cb3eb66',
  clientSecret: '978c5b687161057c41859fda0b35bc17efccca5d',
  repo: 'https://github.com/aoxiaoqiang/aoxiaoqiang.github.io',
  owner: 'aoxiaoqiang',
  admin: ['aoxiaoqiang'],
  id: location.href,      // Ensure uniqueness and length less than 50
  distractionFreeMode: false  // Facebook-like distraction free mode
})

gitalk.render('gitalk-container');
</script>