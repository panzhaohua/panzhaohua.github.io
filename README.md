# Hexo 博客操作

使用git命令，通过github仓库同步；

## 系统需求
使用前必须已安装nodejs和git，推荐使用win10的wsl，配合cmder使用。

## 安装
1. 下载
```
git clone  -b source  git@github.com:panzhaohua/panzhaohua.github.io.git
```
如果已经下载了默认分支，通过
 ``` git checkout -b source origin/source  ```
切换回source分支；不同分支切换使用
 ``` 
git checkout master  
或者 
git checkout source
```


2. 进入目录，安装hexo
```
cd panzhaohua.github.io
npm install hexo
```


## 更新新变动

```
git push  
```
或者
```
git push origin source
```

## 协议

[GPL v3+](LICENSE)