title: Memcached 内存分配
tags: |-

- 内存
- Memcached
- 缓存
  permalink: memcachednei-cun-fen-pei
  id: 15
  updated: '2014-09-23 14:55:03'
  date: 2014-09-04 10:33:15

---

Memcached 是在项目中常使用的分布式缓存服务。很好的解决了 MySQL 数据库的访问压力。所以我们要懂它，用好它。

Memcached 有三个概念：page，slabs，chunk，要理解 Memcached 是如何来存储数据的，那就要理解这三个概念是怎么一回事。

## Page

Memcached 的内存分配是以 page 为单位的，默认情况下一个 page 是 1M 大小。当需要申请内存时，memcached 会划分一个 page 给需要的 slabs 区域。

## slabs

Memcached 不是将所有大小的数据都存在一块的，而是预先划分出不同的区域将不同大小的数据分别存放，这就是 slabs。每个 slabs 只负责存储一定范围大小的数据(由 chunk 决定)。
![](http://blog-geeekr-com.qiniudn.com/images%2F1%2Fdd%2F7eb83f3bdbc5cd9a51ce1976bd22e.png)

## chunk

chunk 是 memcached 实际存放数据的地方，chunk 的大小就是管理它的 slabs 的最大值，所以分配给当前 chunk 的数据都能被存下，如果数据小于当前 chunk 的大小，那么剩余的空间将被闲置，这是防止内存碎片划而设计的。
![](http://geeekr.qiniudn.com/images/e/b8/bbf982ff8eb8979a43ded88d8bbfc.png)

## 内存分配

Memcached 在启动的时候会开辟一块内存(可以通过-m 参数修改)，这些内存是按需分配给 slabs 的。当一个缓存数据需要被存放时，memcached 首选要确定对应的 slabs，如果此 slabs 没有足够空间，那么就要申请空间，申请一个 page 大小的空间，然后按照当前 slabs 的 size(也就是 chunk 的大小)切分成若干个 chunk，然后再将数据存入某一个 chunk 中。
![](http://geeekr.qiniudn.com/images/f/3b/4b8e69e628b00824a5b1b269bab7f.png)

## #slbas 内存分配实例

![](http://geeekr.qiniudn.com/images/1/29/8553a97db78c1805a86e08e40aeca.jpg)
