# 2020年2月24日 推荐新项目——使用nftables实现nat转发

iptables的后继者nftables已经在debain和centos最新的操作系统中作为生产工具提供，nftables提供了很多新的特性，解决了iptables很多痛点。

因此创建了一个新的项目[/arloor/nftables-nat-rust](https://github.com/arloor/nftables-nat-rust)。该项目使用nftables作为nat转发实现，相比本项目具有如下优点：

1. 规则更新是原子的，不会出现规则删不干净的情况——[issue 15](https://github.com/arloor/iptablesUtils/issues/15)
2. 支持端口段转发——[issue 3](https://github.com/arloor/iptablesUtils/issues/3)
3. 转发规则使用配置文件，可以进行备份以及倒入——[issue 14](https://github.com/arloor/iptablesUtils/issues/14)
4. 更加现代（听起来很帅有没有～

所以**强烈推荐**使用[/arloor/nftables-nat-rust](https://github.com/arloor/nftables-nat-rust)。不用担心，本项目依然可以正常稳定使用。

PS: 新旧两个项目并不兼容，因此在两个工具之间切换时，请全新安装指定系统以确保系统纯净。

-----------------------------------------------------------------------------

# 利用iptables设置端口转发的shell脚本

**本项目支持转发到ddns域名、支持udp转发，但不支持端口段转发**

> 用这几个脚本不收费，所以请大家不要觉得我有义务解答脚本使用的问题。有问题请提issue，请不要通过其他途径联系我，下班时间不想被这些事情烦到。

> 老板们，本项目还是在不断开发的，推荐有兴趣的人点star而不是fork，因为fork出的项目是收不到更新的——一个建议而已

很多玩VPS的人都会有设置端口转发、进行中转的需求，在这方面也有若干种方案，比如socat、haproxy、brook等等。他们都有一些局限或者问题，比如socat会爆内存，haproxy不支持udp转发。

我比较喜欢iptables。iptables利用linux的一个内核模块进行ip包的转发，工作在linux的内核态，不涉及内核态和用户态的状态转换，因此可以说是所有端口转发方案中性能最好、最稳定的。但他的缺点也显而易见：只支持IP、需要输入一大堆参数。本项目就是为了解决这些缺点，让大家能方便快速地使用最快、最稳定的端口转发方案。


## 用法

```shell
wget -qO natcfg.sh http://arloor.com/sh/iptablesUtils/natcfg.sh && bash natcfg.sh
```

或

```
wget -qO natcfg.sh https://raw.githubusercontent.com/arloor/iptablesUtils/master/natcfg.sh && bash natcfg.sh
```

输出如下：

```
用途: 便捷的设置iptables端口转发
注意1: 到域名的转发规则在添加后需要等待2分钟才会生效，且在机器重启后仍然有效
注意2: 到IP的转发规则在重启后会失效，这是iptables的特性

你要做什么呢（请输入数字）？Ctrl+C 退出本脚本
1) 增加到域名的转发      3) 增加到IP的转发        5) 列出所有到域名的转发
2) 删除到域名的转发      4) 删除到IP的转发        6) 查看iptables转发规则
#? 
```

此时按照需要，输入1-6中的任意数字，然后按照提示即可

## 致谢

在中秋节收到了平生第一次捐赠，感谢给我捐赠得老板（们）。

表达认可和鼓励只要个位数就行啦，大几十的就千万就不要了！大家钱来得都不容易🙏

## 2020年2月12日 收到一封邮件 心情狂躁

> 你好，你在github的头像是你本人么？
https://github.com/arloor

> 去年上半年时期，我在tg一个叫Netflix讨论群里，和一个头像跟你一样的人py了一个香港解锁NF的节点，
一个月是10块钱，我交了10块，速度也不错，后面用了一周，就显示帐号Deleted，然后节点也不能用了。
我想知道这个人是你么？

从电报找到我的gihub的人，我相信都是因为这个项目。所以，在这个项目的readme加点东西。

我是就上面这个邮件说的人，在我回复他时，我说“解释起来挺复杂，所以不想解释”、“如果需要退10元，回复收款码”、“我再给你个节点，不要钱（已发）”，“不管你信不信，原谅不原谅，别再拿这个事来烦我”。

我“骗了”一个人10元的事情，随便评论吧。我就想说这件事这件事，曾经对我造成了很大的困扰。并且今天，又来了，时隔大概1年。

我想说，是时候结束了。那些被我伤害过的人，对不起，10块钱想拿拿走，节点免费送你。

求你别来了。

念念不忘，必有回响好吧🤮


