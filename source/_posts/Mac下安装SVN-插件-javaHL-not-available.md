title: Mac 下安装 SVN 插件 javaHL not available
tags: |-

- Mac
- SVN
  permalink: install-svn-on-mac-javahl-not-acailable
  id: 9
  updated: '2014-08-21 14:55:42'
  date: 2014-06-16 16:31:37

---

当在 MAC 环境下的 eclipse 安装 subeclipse 插件时会出现如下图所示的错误：

![](http://geeekr.qiniudn.com/images/b/74/33232c351424862ecc68312f4690f.png)

**_说明系统缺少 JavaHL，需要我们手动安装。_**

当然，这并不影响使用，只要选择 SVNKit 方式作为 client。

![](http://geeekr.qiniudn.com/images/6/9a/e44f00181efdde18820d73a0d27b1.png)

但是官方建议使用 JavaHL 作为 client，稳定性，速度都比 SVNKit 好很多。经过实际使用 SVNKit 还会出现未知错误。（javaHL 是通过 jni 的方式来调用本地的 SVN 库，所以说速度快，稳定可靠）

> SVNKit 是 Subversion 的纯 Java 连接库版本，整个连接底层都是由 Java 实现的，不需要额外的支持。而 JavaHL 则使用的是 Subversion 原生的连接库，加上了 Java 调用库。这两种连接库给人表征的感觉应该是 JavaHL 在连接稳定性和速度上应该占优，而 SVNKit 则应该更省事，适用性更广。

## 安装步骤

sbueclipse 官方 wiki 给出来解决方法：[wiki](http://subclipse.tigris.org/wiki/JavaHL)

这里只解释通过 HomeBrew 方式安装：

`brew install --universal --java subversion`

经 geeekr 君亲测这个过程会很漫长。安装完成后，它会提示你：You may need to link the Java bindings…….，然后执行下边的两个 sudo 命令：

```shell
sudo mkdir -p /Library/Java/Extensions
sudo ln -s /usr/local/homebrew/lib/libsvnjavahl-1.dylib /Library/Java/Extensions/libsvnjavahl-1.dylib
```

最后一行会显示 JavaHL 的版本。比如我的就是下边的这个样子：版本号是：1.8.8

![](http://geeekr.qiniudn.com/images/7/dc/c27364deb190b2ee2b4df614b03d4.png)

如果依然有错误，则可能是因为 Subeclipse 和 JavaHL 的版本不对应，[wiki](http://subclipse.tigris.org/wiki/JavaHL)上给出的说明是：

![](http://geeekr.qiniudn.com/images/d/22/928b8434a111152a9aebf878dd0f5.png)

选择对应的版本就 OK 了。
