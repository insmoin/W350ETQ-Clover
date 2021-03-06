# 准系统W350ETQ（神舟K590S）的黑苹果Clover

> 经过了长达半年的折腾。陆陆续续修修补补，终于把这个机型的黑苹果给完善了。此文档主要做备份说明和分享

我目前使用的系统的安装源盘来自远景的[[下载] 【春.之献】macOS High Sierra 10.13.4 17E199 With Clover 4423修正原版镜像](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1780088)，经过数个月的折腾，目前已经做好了该机的Clover配置。我想10.13.x的其他版本系统用这个配置好的clover应该都可以正常安装吧~

## 机器介绍

我是12年10月买的，当时是个准系统，没有品牌，我逢人就说是杂牌，因为A面光板，其他人也看不懂哈哈~有兴趣可以查阅当年写的介绍：

* [Clevo W350ETQ 评测之外观欣赏](https://www.whidy.net/clevo-w350etq-pictures.html)
* [Clevo W350ETQ 评测之跑分测试](http://www.whidy.net/clevo-w350etq-reviews-benchmark.html)
* [Clevo W350ETQ 评测之游戏测试](http://www.whidy.net/clevo-w350etq-reviews-games.html)
* [等等](https://www.whidy.net/?s=W350ET)

主要配置如下：

* 主板：Intel® HM77 Chipset
* 处理器： i7-3612QM (2.10GHz)
* 内存：双通道4G * 2 (DDR3 1600MHz)
* 显卡：Intel® HD Graphics 4000 + NVIDIA® GeForce GTX 660M
* 硬盘：东芝Q200EX 240G
* 显示器：15.6" (39.62cm)  FHD (1920 * 1080), 16:9 Backlit Panel

## 该Clover配置特性

除了以下几点无解，其他功能均为正常。

* 看起来显卡睿频功能暂未实现。
* 主显卡GTX660M无法使用，只能使用核显HD4000并且显存识别为1536MB。
* 自带无线网卡无解，需要第三方无线网卡解决。或者使用有线网络。
* 触摸板勉强能实现部分功能，这个黑苹果不可避免的。
* 有时候自动休眠后，硬盘会进入疯狂读写导致只能强制重启，关闭休眠功能无效，还在尝试解决中。

除以上问题，其他均使用良好。当时最早安装的时候，很多功能都不完善，几乎不能使用，我差点放弃。因为工作繁忙陆陆续续折腾了好几个月，才弄到今天的成果。

## 配置参考资料和一些简单介绍

其实很早就基本上可以使用了黑苹果了，不过当时有几个比较恼人的缺陷：

1. 亮度每次重启都会变的很暗，需要手动调整
1. 处理器频率固定到了2.1GHz，性能很差，Geekbench4大约2200分
1. 无法外接显示器

除了这几个问题，大概还是能用的，之前写过一篇文章，可参阅[Clevo W350ETQ(神舟K590S)安装黑苹果10.13总结](https://www.whidy.net/w350etq-k590s-install-hackintosh-macos-high-sierra-summary.html)

后来又折腾了一些时间，把睿频处理好了，不知道和这个SSDT.AML有无关系，瞎折腾过程中，屏幕亮度也正常了。

关于睿频，我使用了这个工具[ssdtPRGen.sh](https://github.com/Piker-Alpha/ssdtPRGen.sh)，真的很棒，推荐CPU不够睿频，或者说电源管理方面有问题的，可以尝试一下。

而外接显示器，我目前进测试了HDMI外接，1080P屏幕完好。主要是通过Patch来解决的，可能之前的Patch不全就有点问题。至于在哪里搞的Patch，看过太多文章，和测试的补丁，也搞不清究竟是从哪里搞来的O(∩_∩)O~~总之能用就好了。

## 其他

**本项目中的Clover目录或许才对你有用，其他的目录可能不需要使用。**

该笔记本使用时间较长了，所以基本上电池也不怎么耐用了，当成台式机搞搞开发还是可以的。

在进行了很多优化后，目前性能除了显卡- -基本跟Windows下无差，所以性能发挥也是OK的了，请见下图~

![效果预览](Assets/Overview.jpg)

关于Geekbench上面该笔记本普遍分数可参考[Geekbench W350ET](http://browser.geekbench.com/v4/cpu/search?q=w350et)

另外目前该笔记本有个通病，开机要很久才能正常启动，据说换主板电池型号2032可以解决，我换了还是不行（顺便吐槽文具店大姐，竟然卖一个8元，后来才知道淘宝9.8元5个，还包邮，黑店啊），也有可能主板虚焊。

好了，如果还可以的话，我的本本还能再战三年啦啦啦。看了几天的MacBookPro 2018可以省省啦~

如果有疑问欢迎Issue，如果有其他更好的优化方案也欢迎Fork过去PR我啦啦啦~

## 2018年07月31日更新

* 增加了自动启动，我目前开机从按电源键到输入密码，半分钟，速度还是勉强可以的。
* 删除了一些没有用的kexts及其他文件。

> 话说这个上次提到这个笔记本开机反复闪灯，随机时长开机，一开始挺快的只要几分钟，能忍，后来甚至要半小时才能开机，无奈去修，结果修好了，问了下说是重写CMOS，老板也是个老实人，告诉我了（其实就是刷了神舟的BIOS，开机还有个神舟大LOGO，可怕），当时就觉得居然CMOS会影响这种问题，要是一开始我能尝试重刷就好了，因为我也会刷BIOS。不过幸运的是，维修费用150勉强能接受，想起之前跑的两家，第一家280，第二家500，那简直毫无良心。相关贴：
> * [【求助】神舟K590S 不能开机 求高手分析情况](http://tieba.baidu.com/p/3625695588?fid=130154)
> * [K590s反复开关机几十次才能启动](http://tieba.baidu.com/p/5720566188?fid=130154)
> * [关于K590s系列无法开机完整解决方法](http://tieba.baidu.com/p/4689136374)