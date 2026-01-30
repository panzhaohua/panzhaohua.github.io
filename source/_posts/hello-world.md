---
title: Hello World
date: 2019-09-01 11:43:58
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)

---

因为hello world 不添加时间，会自动跟随最近的一篇文章，所以把它时间调整为最旧的文章的前一篇。

因淘宝源换域名，所以更新操作，git下载代码后，加了一下操作
*项目内需要删除旧lock
检查项目根目录是否有 .npmrc 文件，删除或修改它
检查 package-lock.json 是否包含旧镜像地址，如有需要删除后重新生成
 删除锁文件（谨慎操作）*
```
del package-lock.json
npm cache clean --force
npm install -dd
```
安装以后，可以使用以下两种方式执行 Hexo：
`npx hexo <command>`
*Linux 用户可以将 Hexo 所在的目录下的 node_modules 添加到环境变量之中即可直接使用 hexo <command>：*
`echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile`

如果hexo不想加npx,则全局安装命令行，临时使用指定源安装
*单次使用指定源，不修改全局配置*
`npm install -g hexo-cli --registry=https://registry.npmmirror.com`