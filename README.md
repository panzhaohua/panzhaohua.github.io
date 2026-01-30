# Hexo 博客操作
使用git命令，通过github仓库同步；
## 系统需求
使用前必须已安装nodejs和git，推荐使用mobaxterm自带git，配合最新nodejs。
## 安装
1. 下载
```
git clone  git@github.com:panzhaohua/panzhaohua.github.io.git
```

2. 进入目录，安装hexo，加上-dd启用调试模式，方便排查网络问题；
```
cd panzhaohua.github.io
npm install hexo -dd
```
## 更新

```
git push  
```
## 协议
[GPL v3+](LICENSE)

---
因淘宝源换域名，所以更新操作，git下载代码后，加了一下操作
项目内需要删除旧lock
检查项目根目录是否有 .npmrc 文件，删除或修改它
检查 package-lock.json 是否包含旧镜像地址，如有需要删除后重新生成
删除锁文件（谨慎操作）

[del package-lock.json
npm cache clean --force
npm install -dd](https://note.youdao.com/)
安装以后，可以使用以下两种方式执行 Hexo：
[npx hexo <command>](https://note.youdao.com/)
Linux 用户可以将 Hexo 所在的目录下的 node_modules 添加到环境变量之中即可直接使用 hexo <command>：
[echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile](https://note.youdao.com/)

如果hexo不想加npx,则全局安装命令行，临时使用指定源安装
单次使用指定源，不修改全局配置
[npm install -g hexo-cli --registry=https://registry.npmmirror.com](https://note.youdao.com/)

hexo部署参考 [https://hexo.io/zh-cn/docs/github-pages](https://hexo.io/zh-cn/docs/github-pages)