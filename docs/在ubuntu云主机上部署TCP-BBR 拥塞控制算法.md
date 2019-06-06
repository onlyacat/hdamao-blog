## 简介背景
Google 的一项开源的项目。 试了下，对于传输的提升（特别是国外的云服务器）还是极为明显
的，基本上能保证跑满带宽。

[开源地址(github)](https://github.com/google/bbr)

[算法介绍](https://www.zhihu.com/question/53559433)

**注意：BBR 不支持 OPENVZ 的架构**

**注意：使用 BBR 需要升级内核**

## 实际配置(非linode)

代码就两行

```bash
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9-rc8/linux-image-4.9.0-040900rc8-ge
dpkg -i linux-image-4.9.0*.deb
```

完成后需要重启

```bash
sudo poweroff
```

之后开启bbr

```bash
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```

linode的直接在dashboard里切换内核版本后重启就好啦，不需要手动安装

检查

```bash
uname -a
lsmod | grep bbr
```

如果有 tcp_bbr 则大功告成啦
