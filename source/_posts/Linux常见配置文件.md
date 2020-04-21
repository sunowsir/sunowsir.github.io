---
title: Linux常见配置文件
date: 2019-09-02 16:40:04
cover: title.jpg
tags: 
- note 
- 转载
---

> 转载自[CoderZhuang](https://www.cnblogs.com/zxj015/p/4457868.html)，对[CoderZhuang](https://www.cnblogs.com/zxj015/p/4457868.html)先生的博客进行补充和整理。

1. `/etc` 配置文件
    * `/etc/passwd` 用户数据库，其中的域给出了用户名、真实姓名、家目录、加密口令和用户的其他信息 
      * `/etc/group` 类似`/etc/passwd` ，但说明的不是用户而是组。
      * `/etc/inittab` init 的配置文件
      * `/etc/issue` 在登录提示符前的输出信息。通常包括系统的一段短说明或欢迎信息。内容由系统管理员确定。
      * `/etc/motd` 成功登录后自动输出，内容由系统管理员确定，经常用于通告信息，如计划关时间的警告。
      * `/etc/mtab` 当前安装的文件系统列表。由`scripts` 初始化，并由`mount` 命令自动更新。需要一个当前
        安装的文件系统的列表时使用，例如df 命令，当`df –a` 时，查看到的信息应和其一致。
      * `/etc/shadow` 在安装了影子口令软件的系统上的影子口令文件。影子口令文件将`/etc/passwd` 文件中的
        加密口令移动到`/etc/shadow` 中，而后者只对**root** 可读。这使破译口令更困难。
    * `/etc/login.defs` login 命令的配置文件
      * `/etc/profile` , `/etc/csh.login` , `/etc/csh.cshrc` 登录或启动（cshell）时读取的文件（shell不同，文件名称不同，具体查看man手册）。
      * `/etc/printcap` 类似`/etc/termcap` ，但针对打印机。语法不同。
      * `/etc/securetty` 确认安全终端，即哪个终端允许**root**登录。一般只列出虚拟控制台，这样就不可能
        (至少很困难)通过modem 或网络闯入系统并得到超级用户特权。
      * `/etc/shells` 列出可信任的shell。chsh命令允许用户在本文件指定范围内改变登录shell。提供一
        台机器FTP 服务的服务进程ftpd 检查用户shell 是否列在 `/etc/shells` 
        文件中，如果不是将不允许该用户登录。
      * `/etc/termcap`终端性能数据库。说明不同的终端用什么"转义序列"控制。写程序时不直接输出转义序列(这样
        只能工作于特定品牌的终端)，而是从`/etc/termcap`中查找要做的工作的正确序列。这样，多数的
        程序可以在多数终端上运行。
      * `/etc/inputrc` 输入设备配置文件
      * `/etc/default/useradd` 添加用户的默认信息的文件
      * `/etc/login.defs` 是用户密码信息的默认属性
      * `/etc/skel` 用户信息的骨架
      * `/sbin/nologin` 不能登陆的用户
      * `/var/log/message` 系统的日志文件
      * `/etc/profile`全局配置文件可以在添加一行`PATH=$PATH：/usr/local/mysql/bin`即可以软件的命令可以使用
      * `/root/bashrc` 命令的别名
      * `/etc/yum.repos.d` 配置本地yun源(红帽系)
      * `/etc/apt/sources.list.d` 配置本地apt源(debian系)
      * `/etc/httpd/conf/httpd.conf` 配置http服务的配置文件
      * `/etc/fstab` 系统启动时自动加载的设备，（用于配置自动挂载设备）
      * `/etc/selinux` 安全Linux设定
      * `/etc/sysconfig/network` 可以更改`hostname`（主机名）以及网卡工作状态
      * `/etc/hosts` 更改主机名和IP 地址的对应关系，请注意其格式为`hostname.domain` `hostname` `localhost`
        `localhost.domian`，当修改主机名后必须修改该文件
      * `/etc/resolv.conf` 可配置DNS 地址，即第一DNS，第二DNS 以及DNS 的默认搜索路径
      * `/etc/sysconfig/networking/profiles/default` 内含数个文件，可配置hosts、网卡、DNS 地址及
        DNS 搜索路径等
      * `/etc/sysconfig/network-scripts/ifcfg-eth0` 配置网卡eth0(具体名称请使用`ifconfig`查看)
      * `/etc/rc.d/init.d/network restart` 重启网络
      * `/etc/rc.d/init.d` 用于放置几乎所有服务的启动脚本
      * `/etc/sysctl.conf` 内核参数配置文件
         `/etc/sysconfig/i18n`	设置系统语言和字符类型
      * `/etc/crontab` 系统定义的任务计划
      * `/etc/anacrontab` 实现检查过期和未完成的crontab的任务的配置文件
      * `/etc/rc.d/init.d/functions` 定义功能的配置文件
      * `/etc/rc.d/rc.sysinit` 系统启动设置配置文件
      * `/etc/sysconfig/system-config-firewall`配置防火墙的信任端口，以及防火墙的工作状态。图形化配置防火
        墙的存档文件，具体讲只保存图形界面的otherport里面设置的项目，如果主配置
        文件存在相应的配置条目，那么它里面的配置条目存在与否并不重要。
      * `/etc/sysconfig/iptables` 防火墙主配置文件
      * `/etc/sysconfig/system-config-securitylevel` 系统安全等级文件，在防火墙配置中不会涉及
      * `/etc/xinetd.conf xinetd` 的主配置文件
      * `/etc/hosts.allow` TCP的一个许可表
      * `/etc/host.deny` TCP的一个拒绝表
      * `/etc/squid/squid.conf` 代理服务器（SQUID）配置文件
      * `/etc/sysconfig/vncservers` VNC服务配置文件
      * `/etc/vsftpd/ftpusers` 用于保存不允许进行FTP 登录的本地用户账号（黑名单）
      * `/etc/vsftpd/user_list` 更灵活的用户访问控制，但需要在主配置文件中进行声明
      * `/etc/inetd.conf` swat 配置
      * `/etc/dhcpd.conf` DHCP 的配置文件
      * `/etc/rc.d/init.d/dhcpd stop` 停止DHCP
      * `/etc/access` 可以对sendmail 的邮件流进行控制
      * `/etc/udev/rules.d` 系统初始化时将硬件探测信息输出成设备配置文件，是一个程序。
        让用户定义udev的规则，从而实现在创建设备文件使用不同的设备文件名
      * 注：`/etc/passwd` 存放用户的账号，存放形式 ：
        `root:x:0:0:root:/root:/bin/bash` : 
        `用户名：密码位：UID：GID：CECOS(注释)：diectory（家目录）:shell`
      * 注：`/etc/shadow` 存放用户的密码
        `slaceware:$1$12345678$0ME5N6oDyoEAwUp7b5UDM/:15355:0:99999:7:::`
        用户名：加密后的密码：时间1：时间2：时间3：时间4：时间5：时间6：预留段`	
        加密后的密码：以$分开，第一个$后是1，说明加密算法是md5，第二个$后是加的sail，第三个$后是加的密码。
        时间1：从1970年1月1日起到最近的修改的天数
        时间2：密码的最短使用期限
        时间3：密码最长使用期限
        时间4：在密码过期之前多少天开始警告
        时间5：在密码过期多少天用户禁用
        时间6：自1970年1月1日起多长时间用户被禁用
      * 注：`/etc/group` 存放组的账号，存放形式： 
        `slackware:x:5000` : `Name：passwd位置：GID：附加组的用户列表`。
      * 注：
      * 交互式登陆的用户：
        `/etc/profile -->/etc/profile.d/* -->~/.bash_profile -->~/.bashrc -->/etc/bashrc`
    * 非交互式登录：
      /.bashrc -->/etc/bashrc -->.etc/profile.d/*`	
2. `/proc` 配置文件
    * `/proc/dma` 显示当前使用的DMA 通道。
      * `/proc/filesystems` 核心配置的文件系统。
      * `/proc/interrupts` 显示使用的中断，and how many of each there have been.
      * `/proc/ioports` 当前使用的I/O 端口。
      * `/proc/kcore` 系统物理内存映象。与物理内存大小完全一样，但不实际占用这么多内存；
        it is generated on the fly as programs access it. 
        (记住：除非你把它拷贝到什么地方，`/proc` 下没有任何东西占用任何磁盘空间。）
      * `/proc/kmsg` 核心输出的消息。也被送到syslog
      * `/proc/ksyms` 核心符号表
      * `/proc/loadavg` 系统"平均负载"；3 个指示器指出系统当前的工作量。
      * `/proc/meminfo` 存储器使用信息，包括物理内存和swap。
      * `/proc/modules` 当前加载了哪些核心模块。
      * `/proc/net` 网络协议状态信息。
      * `/proc/self` 到查看`/proc` 的程序的进程目录的符号连接。当2 个进程查看`/proc` 
        时，是不同的连接。这主要便于程序得到它自己的进程目录。 
       * `/proc/stat` 系统的不同状态，such as the number of page faults since the system was booted.
      * `/proc/uptime` 系统启动的时间长度。 
      * `/proc/cpuinfo` 处理器信息，如类型、制造商、型号和性能。
      * `/proc/devices` 当前运行的核心配置的设备驱动的列表。
      * `/proc/version` 核心版本。
      * `/proc/mdstat` RAID设备的信息
      * `/proc/cmdline` ro root=/dev/vol0/root rhgb quiet grub信息
      * `/proc/cpuinfo` 显示CPU的相关信息
      * `/proc/cpuset` cpu集合 用于显示当前进程可以应用到哪些cpu上
      * `/proc/filesystem`当前系统支持的文件系统种类
      * `/etc/245/vm` 系统进程ID号为245的进程的虚拟内存信息
      * `/etc/245/kernel` 系统进程ID号为245的进程的内核信息
      * `/proc/mounts` 挂载的所有文件系统
      * `/proc/swaps` 交换分区信息 
      * `/proc/uptime` 启动系统运行时长
      * `/proc/sys` (具有写权限)定义内核参数的值来定义内核的功能
         `/proc/sys/kernel/hostname` 主机名的设定	
3. `/usr` 配置文件
    * `/usr/bin` 众多的应用程序
      * `/usr/doc` linux 文档
      * `/usr/include` linux 下C 开发和编译应用程序所需要的头文件
      * `/usr/include/g++` C++编译器的头文
      * `/usr/lib` 常用的动态链接库和软件包的配置文件
      * `/usr/src` 系统软件的源代码
      * `/usr/src/linux` linux 内核的源代码
      * `/usr/local/bin` 本地增加的命令
      * `/usr/local/lib` 本地增加的库
      * `/usr/sbin` 为系统管理员保留的程序
      * `/usr/share/fonts` 字体文件
      * `/usr/share/doc` 各种文档文件
      * `/usr/share/man` 系统手册页
      * `/usr/local/apache/man` 定义man目录文集
        其它目录配置文件	
      * `/dev/null` 没有用的文件所放的位置，相当于回收站，吞噬设备
      * `/dev/zero` 初始化磁盘（吐零） 
      * `/dev/random` 随机数生成器，熵池
      * `/dev/urandom` 伪随机数生成器，熵池。（当熵池耗尽时，用软件生成随机数）
      * `/var/spool/mail/root` 定义mail设置发送用户为root
      * `/bin/bash` 系统内置脚本
      * `/home/USERNAME` 用户配额文件
      * `/var/spool/cron/USERNAME` 用户定义的任务计划
4. 目录结构：
    * `/boot` 用于自举加载程序（LILO 或GRUB）的文件。当计算机启动时（如果有多个操作系统，
      有可能允许你选择启动哪一个操作系统），这些文件首先被装载。这个目录也会包含LINUX 核（压缩文件
      vmlinuz），但LINUX 核也可以存在别处，只要配置LILO 并且LILO 知道LINUX 核在哪儿。
      * `/bin` 系统启动时需要的引导程序(二进制执行文件)，这些文件可以被普通用户使用
      * `/dev` 代表硬件组件的设备文件目录。LINUX 下设备被当成文件，这样一来硬件被抽象化，便
        于读写、网络共享以及需要临时装载到文件系统中。正常情况下，设备会有一个独立的子目录。这些设备
        的内容会出现在独立的子目录下。LINUX 没有所谓的驱动符。
      * `/etc` 存放各种配置文件
      * `/etc/rc.d` 启动的配置文件和脚本
      * `/home` 用户主目录，包含参数设置文件、个性化文件、文档、数据、EMAIL、缓存数据等
      * `/lib` 标准程序设计库，又叫动态链接共享库，作用类似windows 里的.dll 文件
      * `/sbin` 为系统管理员保留的用于系统启动时的引导程序(二进制执行文件)，这些文件不打算被
        普通用户使用(普通用户仍然可以使用它们，但要指定目录)
      * `/tmp` 公用的临时文件存储点，该目录会被自动清理干净
      * `/root` 系统管理员的主目录
      * `/mnt` 系统提供这个目录是让用户临时挂载其他的文件系统。
      * `/lost+found`这个目录平时是空的，系统非正常关机而留下“无家可归”的文件。
      * `/proc` 虚拟的目录，是系统内存的映射，可直接访问这个目录来获取系统信息。目录整个包含
        虚幻的文件。它们实际上并不存在磁盘上，也不占用任何空间。（用`ls –l` 可以显示它们的大小）当查看
        这些文件时，实际上是在访问存在内存中的信息，这些信息用于访问系统
      * `/proc/1` 关于进程1 的信息目录。每个进程在`/proc` 下有一个名为其进程号的目录。
      * `/var` 某些大文件的溢出区，比方说各种服务的日志文件，包含在正常操作中被改变的文件：
        假脱机文件、记录文件、加锁文件、临时文件和页格式化文件等
      * `/var/spool mail, news`, 打印队列和其他队列工作的目录。每个不同的spool 在`/var/spool` 下有自己的
        子目录，例如，用户的邮箱在`/var/spool/mail` 中。
      * `/opt` 可选的应用程序，譬如，REDHAT 5.2 下的KDE （REDHAT 6.0 下，KDE 放在其它的
        XWINDOWS 应用程序中，主执行程序在`/usr/bin` 目录下）
      * `/usr` 最庞大的目录，要用到的应用程序和文件几乎都在这个目录。
      * `/home /var /usr/local` 经常是单独分区，因为经常会操作，容易产生碎片
      * `/srv` 该目录存放一些服务启动之后需要提取的数据
