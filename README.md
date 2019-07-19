# npm
* npm常用命令

```bash
npm list  // 查看本地已安装模块清单
npm list [packageName] // 查看本地已安装模块版本
npm info [packageName] //查看模块的详细信息 包括各版本号等
npm view [packageName] version // 查看模块远程最新版本
npm view [packageName] versions // 查看模块远程所有版本
```

* npm scripts 使用指南  
http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html


# ECMAScript 6 入门
*  Module 的语法  
http://es6.ruanyifeng.com/#docs/module


# Vue
* 包学会之浅入浅出 Vue.js：开学篇  
https://juejin.im/entry/58df6632a0bb9f0069e3ad04

# MacBook
* 查看环境变量
```bash
$ echo $PATH
```

* 修改环境变量
```bash
$ vim ~/.bash_profile

export PATH=/usr/local/mysql/bin:/Users/zhaoxm/bin/apache-maven-3.6.1/bin:$PATH

```

注：如果编辑profile文件没有写正确，会导致在命令行下vim touch等命令不能够识别如报错：vim: command not found

解决办法：直接在终端执行以下命令即可解决：
export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin

https://www.cnblogs.com/vitasyuan/p/7395601.html?utm_source=debugrun&utm_medium=referral
