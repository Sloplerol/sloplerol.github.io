---
title: "Linux"
date: 2023-02-28T17:38:53+08:00
draft: false
---
## Linux

* ⚙️[操作系统发展史](#1)
    * [Unix](#unix)
    * [Minix](#minix)
    * [早期Linux](#linux)
* ⚡️[Linux介绍](#2)
    * [Kernel](#kernel)
    * [Releases](#releases)
    * [Unix目录](#unixcategory)
    * [Linux目录](#linuxcategory)
    * [Vim和VI文本编译器](#Vim)
        * [Vim和VI是什么](#whatvim)
        * [VIM的模式](#vimmodel)
    * [主机与虚拟机联系](#connect)
        * [测试是否主机和虚拟机之间是否能ping通](#test)
        * [VMware提供三种网络连接方式](#network)
        * [指定修改静态ip](#alterip)
        * [修改IP出现的问题](#breakdown)
        * [修改主机名](#hostname)
    * [进程与服务](#service)
    * [Linux运行级别](eposide)
    * [关机重启操作](#reboot)
* 💥[Linux命令的使用](#3)
    * [基本介绍](#introduction)
    * [拓展](#expansion)
    * [帮助型命令](#help)
    * [文件目录类](#filecategory)
    * [时间日期类](#date)
    * [用户管理类](#usermanage)
    * [搜索查找类](#search)
    * [解压缩类](#gzip)
    * [磁盘查看和分区类](#diskdetect)
    * [进程管理类](#process)
    * [软件包管理](#software)
    * [克隆虚拟机](#clone)
* 🔥[Shell的拓展](#4)
    * [Shell巩固(命令解释器)](#shell)
    * [Shell脚本](#scripts)
    * [读取控制台输入](#console)
    * [函数](#function)
    * [正则表达式](#Regular-expression)
    * [文本处理工具](#texthandle)
    * [巩固](#review)

<p id="1"></p>

### 操作系统发展史

<p id="unix"></p> 

**Unix**

* 1965年左后由贝尔实验室、麻省理工学院 以及 通用电气共同发起了Multics项目，**想让大型主机支持300台终端**

* 1969年前后这个项目进度缓慢，资金短缺，贝尔实验室退出了研究
* 1969年从这个项目中退出的Ken Thompson当时在实验室无聊时，为了让一台空闲的电脑上能够运行“星际旅行”游行，在8月份左右趁着其妻子探亲的时间，用了1个月的时间编写出了 Unix操作系统的原型
* 1970年，美国贝尔实验室的 Ken Thompson，以 BCPL语言 为基础，设计出很简单且很接近硬件的 B语言（取BCPL的首字母），并且他用B语言写了第一个UNIX操作系统。
    因为B语言的跨平台性较差，为了能够在其他的电脑上也能够运行这个非常棒的Unix操作系统，Dennis Ritchie和Ken Thompson 从B语言的基础上准备研究一个更好的语言
* 1972年，美国贝尔实验室的 Dennis Ritchie在B语言的基础上最终设计出了一种新的语言，他取了BCPL的第二个字母作为这种语言的名字，这就是C语言
* 1973年初，C语言的主体完成。Thompson和Ritchie迫不及待地开始用它完全重写了现在大名鼎鼎的Unix操作系统

<p id="mixin"></p>

**Minix**

> 由于Unix的私有化，Andrew S. Tanenbaum(塔能鲍姆)教授自行开发与UNIX兼容的操作系统，为了避免和Unix版权上的争议，起名为mini-unix，即Mixin

<p id="linux"></p>

**Linux**

> 因为Minix只是教学使用，因此功能并不强，因此Torvalds利用GNU的bash当做开发环境，gcc当做编译工具，编写了Linux内核-v0.02，但是一开始Linux并不能兼容Unix，即Unix上跑的应用程序不能在Linux上跑，即应用程序与内核之间的接口不一致因为Unix是遵循POSIX规范的，因此Torvalds修改了Linux，并遵循POSIX（Portable Operating System Interface，他规范了应用程序与内核的接口规范）； 一开始Linux只适用于386，后来经过全世界的网友的帮助，最终能够兼容多种硬件

```html
<p id="2"></p>
```

### Linux介绍

<p id="kernel"></p> 

* Kernel(内核)

    内核分为两个版本

    * 稳定版：长期稳定版
    * 开发版：变更很快

    <p id="releases"></p> 

* 发行版

    市面上比较常见的有

    * Ubantu
    * Centos
    * Debain
    * SuSe
    * RedHat

    <p id="unixcategory"></p> 

* 类Unix系统目录结构

    ![Category_struct](/Users/satrol_/Desktop/Category_struct.png)

    <p id="linuxcategory"></p> 

* Linux目录结构

    ![](/Users/satrol_/Desktop/Linux_struct.jpeg)

    * / : Linux下只有一个根目录，指的就是/home
    * /bin: 可执行二进制文件的目录，如常用的命令ls、tar、mv、cat等 实际存储于usr/bin
    * /boot: 启动时用到的一些文件 如Linux的内核文件：/boot/vmlinuz，系统引导管理器：/boot/grub。
    * /dev: 存放linux系统下的设备文件 常用的是挂载光驱 mount /dev/cdrom /mnt。
    * /etc: 系统配置文件存放的目录
    * /home: 系统默认的用户家目录，新增用户账号时，用户的家目录都存放在此目录下
    * /lib: 系统使用的函数库的目录，程序在执行过程中，需要调用一些额外的参数时需要函数库的协助。
    * /lost: 系统异常产生错误时，会将一些遗失的片段放置于此目录下。
    * /mnt /media: 光盘默认挂载点，通常光盘挂载于 /mnt/cdrom 下，也不一定，可以选择任意位置进行挂载。
    * /opt: 给主机额外安装软件所摆放的目录。
    * /proc: 此目录的数据都在内存中，如系统核心，外部设备，网络状态，由于数据都存放于内存中，所以不占用磁盘空间
    * /root: 系统管理员root的家目录
    * /sbin: 放置系统管理员使用的可执行命令，如fdisk、shutdown、mount 等。与 /bin 不同的是，这几个目录是给系统管理员 root使用的命令，一般用户只能"查看"而不能设置和使用。
    * /tmp: 一般用户或正在执行的程序临时存放文件的目录
    * /srv: 服务启动之后需要访问的数据目录
    * /usr: 应用程序存放目录
    * /var: 放置系统执行过程中经常变化的文件，如随时更改的日志文件 /var/log，/var/log/message：所有的登录文件存放目录，/var/spool/mail：邮件存放的目录，/var/run:程序或服务启动后，其PID存放在该目录下
    * /sys：存放系统硬件相关信息

    <p id="Vim"></p> 

* 文本编译器VIM

    <p id="whatvim"></p> 

    * Vim和VI是什么

        VI 是Unix和类Unix操作系统通用的文本编译器

        **VIM ** 是由VI发展过来更加强大的文本编译器

        两者完全兼容

        <p id="vimmodel"></p> 

    * VIM的模式

        * 一般模式(可执行操作：撤销，复制，删除)

            * 撤销: u

            * 复制: yy

                ```
                复制光标及当前行以后的内容
                y + $
                复制光标及当前行之前的内容
                y + ^
                复制某一个单词
                y + w  按下w可以跳转到下一个单词
                ```

                

                

            * 粘贴: p 

                ```
                粘贴多行
                Linux Learning
                ex: 加入我想粘贴Linux Learning粘贴这一行三次
                进入一般模式按下数字再按下p即可完成这部操作
                ```

            * 删除: dd

                ```
                删除多行
                数字+dd
                删除一个单词
                d + w
                	当光标在当前词的最前面删除的是整个单词
                	当光标在单词中会删除拆解出来的单词及后面的空格
                删除光标前的内容
                d + $
                删除光标后的内容
                d + ^
                剪切光标处在的位置
                x
                一般模式下的退格键
                大写X
                ```

            * 切换文字大小写(~)

            * 替换 

                > shift + r进入替换模式

            * 快速跳转

                ```
                跳转行头
                shift + 6
                跳转行尾
                shift + 4
                跳转至下一个单词
                w
                跳转至上一个单词
                b
                跳转至文档开始的地方
                gg 或者 H
                跳转到文档行尾
                G 或者 L
                跳转文档开始和结束可以结合数字
                ```

        * 编辑模式

            * i 在光标前进行编辑
            * a 在光标后进行编辑
            * o 在光标下一行进行编辑
            * I 跳转到当前行头并进行编辑
            * A跳转到当前行尾进行编辑
            * O跳转到当前行的上一行进行编辑

        * 指令模式

            * 进入方式:  **:** or **/**

            * :w 保存

            * :q 退出

            * :wq 保存并退出

            * :q! 不保存强制退出

            * :set nu 显示行数 

            * :set nonu 关闭行数

            * / + 关键字 = 查找 按n查找下一个  N查找上一个

            * 取消高亮  :noh

            * 替换关键词

                * 替换当前行第一个关键词

                    ```
                    :s/想替前的词/替换后的词
                    ```

                * 替换当前行全部关键词

                    ```
                    :s/想替前的词/替换后的词/g
                    ```

                * 替换每一行第一个关键字

                    ```
                    :%s/想替前的词/替换后的词
                    ```

                * 替换整篇文档全部的关键字

                    ```
                    :%s/想替前的词/替换后的词/g
                    ```

    <p id="connect"></p> 

* 主机与虚拟机的联系

    <p id="test"></p> 

    * 测试是否主机和虚拟机之间是否能ping通

        ```
        window
        ipconfig查询本机ip
        Linux虚拟机
        对应系统执行相应ip
        inet : 网络地址
        broadcast : 专门用于同时向网络中所有工作站进行发送的一个地址
        ```

        <p id="network"></p> 

    * VMware提供三种网络连接方式

        * 桥接模式

            原理: 路由连接外网，通过DHCP服务器，动态分配ip地址，这些设备形成的网络叫做局域网

            VM虚拟机连接外网方式：路由器通过PC虚拟出来的网桥连接到交换机，再通过交换机来分配多台vm设备

            缺点: 没有隐私性，当前网络段下的pc设备都能访问其隐私，占用ip

        * NAT模式(vmnet8)

            原理: PC连接到虚拟机虚拟出来的路由,虚拟路由动态分配ip给每一台vm设备形成一个虚拟局域网(这就是为什么虚拟机ip可以和本机ip不在一个网段上的原因，位于两个不同的局域网)

            vmnet8: 但是如果想要PC连接到vm设备就好比外网连接PC，只能获取到简单的路由ip而不能准确定位到你本机ip，于是vmware虚拟出来一张虚拟网卡供PC使用来确定是哪一台vm设备，也就是所谓的vmnet8

            

        * 仅主机模式(vmnet1)

            原理: PC通过虚拟网卡连接交换机，并且与其余vm构建局域网，由于是交换机与pc打交道所以vm设备无法访问到外网   

        * 总结

            > 虚拟路由通过NAT转址为本机ip，本机访问外网同理通过路由转址为外网ip进行访问

            <p id="alterip"></p> 

    * 指定修改静态ip

        ```
        进入局域网段里ens160(mac) or ens33(window)
        vim /etc/sysconfig/network-scripts/ifcfg-ens160
        
        修改内容:
        Bootproto: static
        IPADDR: 相同网段
        GATEWAY: 于虚拟及NAT设置网关相同
        DNS1: 与GATEWAY一致
        保存
        :wq
        重启
        service network restart
        ```

        <p id="breakdown"></p> 

    * 修改IP出现的问题

        * 主机能ping通虚拟机而虚拟机ping不通主机

            > 可能是主机防火墙干扰

        * 虚拟机可以ping通主机但是连不上外网

            >  DNS设置出错
            >
            >  检查是否子网ip和NAT网关存在一个网段上

        * 如果以上方法都不行可以选择关闭NetworkManager

            ```
            systemctl stop NetworkManager //停止服务
            systemctl disable NetworkManager //禁止服务
            ```

            <p id="hostname"></p> 

    * 修改主机名

        * VIM到当前目录下

            ```
            vim /etc/hostname
            重启服务
            hostnamectl set-hostname 需要修改的名
            ```

        * 设置 主机-ip

            ```
            进入hosts
            vim /etc/hosts
            ```

        * 修改本机hosts文件夹

            ```
            172.20.10.12 sparking2
            172.20.10.13 sparking3
            172.20.10.14 sparking4
            172.20.10.15 sparking5
            172.20.10.16 sparking6
            目的：实现对服务器的远程操作和连接
            ```

        * ssh远程登陆

            ```
            远程连接
            window Xshell mac iTem2
            ssh root@host名/ip地址
            远程下载或者上传
            window xftp mac FileZilla 
            ```

        <p id="service"></p> 

    * service 服务管理

        服务：常驻内存中的进程

        进程：正在执行的程序和命令

        > 以d为结尾的目录为守护进程

        Centos6 

        ```
        service + start/stop/status/restart
        重启服务
        service network restart
        ```

        Centos7

        ```
        systemctl + start/stop/status/restart
        服务管理文件目录
        ls /usr/lib/systemd/system
        重启服务
        systemctl restart network
        建议在network和NetworkManager里选择一个进行保留
        ```

        <p id="eposide"></p> 

    * Linux运行级别

        > 查看默认级别 vim /etc/inittab

        **运行步骤**: 开机->BIOS->/boot->/init进程->运行级别->运行级别对应的服务 

        级别0: 系统停机状态

        级别1: 只允许root登陆 不支持远程登录

        级别2:  多用户状态 无NFS 但没网

        级别3: 完全多用户状态 有NFS 相当于命令行模式

        级别4: 保留未使用

        级别5: GUI窗口化模式

        级别6: 重启

        ```
        Centos7将级别三服务简化为multi-user.target
        将级别5简化为graphical.target
        查看当前级别
        systemctl get-default
        如果有graphical.target和multi-user.target两个级别
        可以通过init + 级别进行切换
        ```

        Centos6启动服务前先启动init文件 单线程启动

        ```
        启动Centos6 SysV服务
        chkconfig --list
        关闭开启network开机自启动服务
        chkconfig network off/on
        针对单个级别进行关闭
        chkconfig --level 3 network off
        防火墙
        iptables
        ```

        

        Centos7启动服务前先启动systemd文件 并行启动

        ```
        调整开机自启动状态
        setup 进入服务面板
        开启/关闭开机自启动服务
        systemctl disable/enable 某一个服务
        列举所有单元
        systemctl list-unit-files
        enable代表开机自启动 disable反之 static代表无法确定
        查看防火墙状态
        systemctl status firewalld
        关闭防火墙
        systemctl stop firewalld
        ```

        <p id="reboot"></p> 

    * 关机重启操作

        ```
        一分钟后关机(default)
        shutdown
        shutdown + number 几分钟后关机
        shutdown + 具体时间 某一时间关机
        停止关机操作
        shutdown -c
        立刻关机
        shutdown now
        将缓冲区的数据立刻读取到硬盘中
        sync
        关闭系统但不断电
        halt
        关闭系统且断电
        poweroff
        重启
        reboot
        ```

```html
<p id="3"></p>
```

### Linux命令基本使用

<p id="introduction"></p> 

* 基本介绍

    Shell 是一个应用程序，它连接了用户和Linux 内核，让用户能够更加高效、安全、低成本地使用Linux 内核

    <p id="expansion"></p> 

* 拓展

    命令行的打开都是基于/bin/sh

    Unix 最原始的shell是Bourne shell 不过用户交互性较差

    Linux基于Unix 开发出Bourne Again shell 即bash

    Debian系列搭载的shell是dash

    <p id="help"></p> 

* 帮助型命令

    * man查看命令手册

        ```
        man + 你想要查看的命令
        内嵌命令：内嵌在bash里面 ex:cd/exit/history
        type查看命令类型
        如果想要查看内嵌命令 里面可能会有不同版本的解释 
        man -f + 内嵌命令
        man + 版本 + 内嵌命令 查看当前版本的解释
        help查看内嵌命令
        help + 内嵌命令
        help查看外部命令
        外部命令 --help
        ```

    * 常用快捷键

        Ctrl + c 停止进程

        Ctrl + l 清屏

        reset 重新启动shell

        上下键快速补齐之前的命令

        <p id="filecategory"></p> 

* 文件目录类

    * pwd显示当前绝对路径

    * 绝对路径

        从根目录开始定位到当前目录的整体路径

        ex： 我在中国哪个省哪个市。。。 

    * 相对路径

        从现在的位置去定位目标位置

        ex： 我在北京我要去哪个市 基于北京直接cd这个市

        > ../返回上一级目录
        >
        > cd -返回上一次定位的目录
        >
        > cd直接回到主文件夹
        >
        > Ex: cd /home/hello    cd=>/home
        >
        > 切换用户
        >
        > su + 用户名
        >
        > 当前根目录随之发生改变

    * 列举文件

        * ls-a 

            显示当前目录下所有文件包括隐藏文件

        * ls -l / ll

            显示当前目录可视化文件的全部信息 包括权限创建时间文件名等等

        * 上两者可以合并 ls -al

    * 创建目录

        ```
        mkdir + 文件名 //在相对路径下创建一个或多个文件
        ex: mkdir a  mkdir /a   mkdir a a/b a/b/c 
        ```

    * 删除空文件

        ```
        rmdir + 文件名 
        注意: 如果删除的文件下面还有文件则删除失败
        如果想要删除一个嵌套文件夹
        rmdir -p a/b/c  删除c若发现b目录文件夹下为空则再删除b
        ```

    * 创建一个空的文件夹

        ```
        touch + 文件夹名
        touch + 具体路径/文件夹名
        ```

    * 复制文件到指定路径下

        ```
        cp 当前目录下的文件名 目标路径
        如果后面填写的是一个文件会对其进行覆盖
        或者虽然是目标路径但是里面已经有你想cp的文件也会出现覆盖选项
        如果想要直接对其进行覆盖在cp前加上\
        ```

    * 复制目录到指定路径下

        ```
        cp -r 目录 复制到的目标路径 //-r递归复制目录下的所有文件
        ```

    * 删除文件

        ```
        rm本质上操作相当于是rm -i 交互式
        rm + 文件名
        强制删除
        rm -f + 文件名
        删除目录
        rm -r + 目录名
        直接删除目录且没有提示
        rm -rf + 目录名
        删除当前目录及以下的所有文件（小心使用）
        rm -rf /
        删除当前目录下的所有文件
        rm -f ./*
        ```

    * 移动文件

        ```
        mv 当前文件 目标路径
        mv 当前文件 目标路径/重命名
        如果处于root文件夹下
        mv 文件名 重命名后的名 可以直接实现重命名
        ```

    * 查看文件内容

        ```
        cat 文件名
        cat -n 文件名 //显示每一行的行号
        more 文件名 //全屏查看 空格下一篇 enter下一行 b上一行 :f显示当前行数 q直接退出
        less 文件名 //比more更强大的查看方式
        ```

        

    * 输出重定向

        ```
        echo + 想要输出的内容
        想要显示多空格
        echo + "想要输出的内容"
        支持转义
        echo -e "想要输出的内容"
        通过echo写入将内容写入到文件中
        ll > info //将ll里的内容写入到info下
        ls > info //由于info里面有内容所以将ls里的内容覆盖info
        如果想要追加内容
        echo "hello world" >> info
        查看环境变量
        echo $环境变量名
        环境变量概念: 当前目录下通过环境变量调用指定命令可以直接输出结果
        ```

    * head显示头部内容

        ```
        head 文件名 //显示文件的前十行
        head -n 显示的行数 文件名 显示文件的前n行
        ```

    * tail显示尾部内容

        ```
        tail 文件名 //显示文件的前后十行
        tail -n 显示的行数 文件名 显示文件的后n行
        tail -f 文件名 //对该文件内容进行监测 ctrl+暂停监控
        监控是通过每一个文件的索引号来实现的
        ls -i 文件名 查看该文件的索引号
        vim 对文件操作实质上索引号发生了改变
        ```

        

    * 软链接

        * 概念: 和桌面快捷方式一致，点击会去连接到某一路径下的某个程序，/bin =>/usr/bin

        * 创建或删除软链接

            ```
            ln -s /想链接的文件或者是路径 软链接名称或者某个路径下软链接名称
            vim软链接，之前文件的内容也会发生改变
            如果在软链接下想要看到物理路径
            pwd -P
            删除软链接
            rm + 软链接名称 不会删除原文件
            删除原文件夹下的所有文件
            rm -rf 软链接名 + /
            如果把原文件删除 那么软链接将不复存在
            ```

        * 硬链接

            > 原文件和其他链接去连接innode元信息，元信息再去内存中进行查找，就算原文件删除了还是能通过别的链接获取内存数据

    * 历史记录

        ```
        history 查看所有输入过的历史记录
        history + 数字 显示刚刚输入的n条命令
        !行数 显示在这一行所输入的命令
        history -c 清空历史记录
        ```

    <p id="date"></p> 

* 时间日期类

    * date

        ```
        date 显示所有时间信息
        date +%Y //显示当前年份
        date +%y //显示当前年份后两位
        date +%m //显示当前月份
        date +%d //显示当前天数
        date +%s //显示时间戳
        date -d "1 days ago" //显示明天这个时间
        date -s "系统时间" //设置系统时间
        npdate可以同步国家系统时间
        ```

    * cal

        ```
        cal 查看日历
        cal -数字 查看临近的几个月
        cal -m 将周一放到第一天
        cal 年份 查看当年的全部信息
        ```

        <p id="usermanage"></p> 

* 用户管理类

    * 添加用户

        ```
        默认情况下有两个用户 root管理员用户 普通用户存放于/home下
        添加用户
        useradd 用户名
        更改home下用户名的主文件夹名 用户名还是david
        useradd -d /home/dava david
        添加用户的同时添加组
        useradd -g 已有的组名 用户名
        为用户设置密码
        passwd 用户名
        ```

    * 查询用户

        ```
        查询用户是否存在
        id 用户名 uid用户id gid组id
        想要查看所有用户
        cat /etc/passwd
        ```

    * 切换用户

        ```
        su 用户名
        exit退出到上一级用户
        ```

    * 查看自己是哪一用户

        ```
        who am i //返回结果为根用户
        whoani //返回当前用户
        ```

    * sudo临时赋予最高管理员权限

        ```
        想要使用sudo命令需要添加至sudoers
        su root 1/
        vim /etc/sudoers
        Y到最后 复制root添加权限那行
        粘贴修改用户名为你创建的普通用户
        :wq!强制保存
        现在你就在你添加的用户里可以使用sudo
        sudo + 想要执行的命令
        ```

    * 删除用户

        ```
        userdel + 用户名 //用户删除但是文件夹残留
        userdel -r 用户名 //用户和用户文件夹全部删除
        ```

    * 查看组别信息

        ```
        cat /etc/group
        ```

    * 创建组

        ```
        groupadd 组名
        ```

    * 修改用户所处的组

        ```
        usermod -g 组名 用户 //将用户添加到这组
        ```

    * 修改组名

        ```
        groupmod -n 新的组名 旧的组名
        ```

    * 删除组

        ```
        groupdel 组名
        ```

    * wheel组

        > wheel组属于管理组 可以使用sudo命令

    * 文件属性和权限

        ```
        ls -l 或者ll 一个文件的属性
        查看属性显示的内容依次是
        文件类型-属主权限-属组权限-其他权限 number
        属主权限(u)： root权限 
        属组权限(g)： 当前组下的权限 
        其他权限(o)： 别人访问时候的权限
        a: 代表所有权限
        number: 代表硬链接的数量至少要一个
        mkdir创建出来的目录至少有两个硬链接一个是本身还有一个是父目录
        ```

        作用到文件

        * r可以对文件进行读取
        * w可以对文件进行修改
        * x可以cd该文件

        作用到目录

        * r可以读取查看文件内容
        * w可以对文件进行增删改查的目的
        * x可cd到该目录

    * 更改用户权限

        ```
        chmod (u/g/o/a)(=+-)(r/w/x) 文件名
        分别添加权限
        ```

        **技巧**

        x: 1 w:2 wx: 3 r: 4 rx:5 rw:6 rwx:7

        相当于是二进制 111 => 7 rwx

        Chmod 777 指定文件 开启全部权限

        一般设置文件都设置为644 rx-r--r--

        > chmod -R 777 文件 将当前目录下的所有文件都设置为777

    * 更改所属主和所属组

        ```
        更改所属主
        chown 想要修改的用户 文件名/目录
        +R 遍历目录下所有文件
        ```

        ```
        更爱所属组
        chgrp 想要修改的组别 文件
        ```

    * 团队合作流程

        ```
        创建一个组两个人同时链接这个组
        通过权限的开与关从而实现数据交互性
        如果要给外人传递数据开放其他权限即可
        ```

        <p id="search"></p> 

* 搜索查找类

    * find查找(从硬盘上去查找)

        ```
        find -name 文件名 //查找当前目录及下的所有文件
        find 路径 -name 文件名 //查找该路径下的所有文件
        find -name "*.cfg" //查找其下的所有带有cfg的文件
        find /home -user 用户名 //查找所有与该用户相关的文件
        ls -lh 查看文件时文件大小显示的更加详细
        find /root -size +2M //查看当前目录下大小超过2M的文件
        ```

    * locate查找(快速从数据库内进行查找)

        ```
        实时更新
        updatedb
        查找
        locate 关键字
        查找命令真实路径
        which + 命令名
        where + 命令 相比于which更加详细
        ```

    * grep查找

        ```
        grep -n 关键字 文件名     -n显示行号
        灵活运用|来进行筛选
        ls | grep .cfg //将ls返回的结果作为后面语句的参数
        wc可以用来得到一个文件的详细信息
        wc 文件 得到的结果分别是总行数 总单词数 总字节数
        ```

        <p id="gzip"></p> 

* 解压缩类

    * gzip

        ```
        gzip 文件 压缩
        gunzip 文件 解压
        特点
        可以同时解压多个文件但是都是单独生成的
        不会保留原来的文件
        不能压缩目录
        ```

    * zip

        ```
        zip -r total.zip 要压缩的文件或者是目录
        unzip -d 指定路径 解压的文件
        ```

    * tar

        ```
        -c 产生.tar文件
        -z 打包并压缩
        -v 显示详细信息
        -f 指定压缩后的文件名
        -x 解包
        -C 解包指定目录
        打包
        tar -zcvf 文件名.tar.gz 打包的文件可以是多个
        解包
        tar -zxvf 文件名 -C 解包路径
        ```

        <p id="diskdetect"></p> 

* 磁盘查看和分区类

    * 查看磁盘占用情况

        ```
        du 目录/文件
        -a 查看子目录大小和文件大小
        -h 将大小转化为KB MB
        -c = -ah
        -s 只显示总量
        --max-depth = n //n代表文件的深度
        ```

    * 查看磁盘空间的占用情况

        ```
        df -h
        硬盘分类默认分为3个区 swap/boot/根目录
        ```

    * 查看内存占用情况

        ```
        free -h
        Mem: 物理内存
        Swap: 虚拟内存
        ```

    * 查看设备挂载情况

        ``` 
        lsblk
        硬盘分类
        IDE 老式硬盘 => hda
        SATA 容量大 成本低
        SCSI 拓展性广 传输速度快
        sata和scsi对应的都是sda
        显示文件系统信息
        lsblk -f
        ```

    * 挂载卸载

        ```
        挂载
        mount /dev/cdrom /mnt/cdrom //将dev下的光盘挂载到mnt下
        卸载
        umount /dev/cdrom  同时也卸载了mnt/cdrom里的内容
        开机自启动
        vim /etc/fstab //进入到挂载区域
        在新的一行填写
        想要挂载谁 挂载到谁身上 文件系统类型(默认iso9660) defaults 0 0
        ```

    * fdisk分区

        ```
        查看分区信息
        fdisk -l
        对磁盘进行管理
        fdisk 磁盘目录(可以通过fdisk -l来查看)
        m进入 n划分新磁盘 p查看磁盘分区 w保存磁盘设置并退出
        初始化新磁盘信息
        mkfs -t xfs 磁盘的那一块分区
        将磁盘进行挂载
        mount /dev/sda1 /home/用户
        //卸载
        umount /home/用户
        df -h没有新磁盘的数据
        lsblk -f还保留着
        ```

        <p id="process"></p> 

* 进程管理类

    * ps

        ```
        ps //列出当前用户进程状态
        -e 列出所有进程
        -u 列出某个用户所有进程
        -f 显示完整格式的进程列表
        ps aux 查看所有用户的所有进程
        VSZ：虚拟内存 长时间未使用的命令就会放到其中
        RSS：物理内存 经常使用的
        TTY：代表哪一个终端 tty1图形化终端 tty2-6黑屏 pts/ 虚拟终端
        STAT：S睡眠 T暂停 Z僵尸 s子进程 l多线程 +前台显示
        ps -ef 显示标准用户进程
        PIDD 副进程需要父进程先启动才能启动该进程
        ps aux 用来查看资源占用率
        ps -ef 用来查看父子进程关系
        ```

    * 查看远程登录进程

        ```
        ps -ef | grep sshd
        /usr/sbin/sshd -D是sshd远程登录的父进程
        grep --color=auto sshd所运行的进程的父进程是bash的主进程
        ```

    * 终止进程

        ```
        kill + PID/PPID
        如果终止的是守护进程 那么远程服务器就链接不到了 但是不影响已经登录上来的进程，需要在已登陆的进程上开启sshd服务
        systemctl start sshd
        如果想要kill 正在运行的bash终端 需要强制删除
        kill -9 PID
        删除所有与关键字有关的服务
        killall 关键字
        ```

    * 查看进程树

        安装

        ```
        yum install psmisc #using psmisc package for pstree
        ```

        使用

        ```
        pstree //查看进程树
        pstree -p //带有PID
        pstree -u //带有用户信息
        ```

    * top实时监视系统状态

        ```
        top -d 秒数 几秒刷新一次
        top -i 不显示闲置或者是僵死转台的数据
        top -p PID 监视单个进程
        u 指定监视的用户
        k 指定杀死用户
        ```

    * netstat显示网络状态和端口占用信息

        ```
        套接字: iP + 端口
        netstat -anp 查看网络状态
        netstat -alp 查看端口状态
        ```

    * crontab定时任务管理

        * 前提: 需要将crond 打开

            ```
            systemctl start crond
            ```

        * 操作

            ```
            -l 查看定时任务
            -e 编辑定时任务
            -r 删除定时任务
            ```

        * 参数说明

            ```
            * * * * * + 命令
            第一个：一小时的哪一分钟
            第二个：一天的哪一个小时
            第三个：哪一天
            第四个：哪一个月
            第五个：星期几
            tail -f 文件名 //用来监视后添加的文本
            ```

            <p id="software"></p> 

* 软件包管理

    * RPM概念

        > RedHat软件包管理工具，

    * 查询安装过的RPM包

        ```
        rpm -qa
        rpm -qi 软件名 //查看安装软件的详细信息
        ```

    * 卸载软件

        ```
        rpm -e RPM包
        rpm -e --nodeps 软件包 //不检查依赖直接卸载
        ```

    * 安装软件

        ```
        rpm -i RPM包全名 需要到cdrom package里去查找 可能会由于没有依赖而安装失败
        ```

    * yum

        * 语法说明

            > yum [需要进行的操作] 软件包名称

        * 删除rpm包

            ```
            yum remove rpm包
            yum install rpm包
            yum list rpm包 //查看安装完的所有包
            ```

        * 修改镜像源

            ```
            文件目录为/etc/yum.repos.d/CentOS-Base.repo
            步骤一 
            yum install weget
            步骤二
            wget aliyun/网易国内Centos.repo文件
            步骤三
            替换: cp 下载下来的文件 原来centos文件备份
            ```

            <p id="clone"></p> 

* 克隆虚拟机

    * 到达虚拟机资源库右键克隆完整虚拟机

    * vim 到ens160下修改ip地址

        ```
        注意 此ip和之前在本机host文件配置某一ip一致
        下面设置主机名需要与该ip进行匹配
        ```

    * NetworkManager是网络通信的关键所以可以暂停network服务

        ```
        systemctl stop network
        systemctl restart NetworkManager
        ping 本机
        ping 外网
        ping通开始下一步
        ```

    * 更改主机名

        ```
        hostnamectl set-hostname 需要修改的名
        ```

```html
<p id="3"></p>
```

### Shell拓展

<p id="shell"></p> 

* Shell巩固(命令解释器)

    > Shell最初的版本是Unix的BourneShell
    >
    > 最底层是硬件，操作系统内核来操作硬件，用户处于应用层，由于内核不能理解用户的各项操作，所以衍生出Shell来为用户的操作做出解释

    查看Linux提供的命令解释器

    ```
    cat /etc/shells
    ```

    查看现在应用的shell

    ```
    echo $SHELL
    ```

    <p id="scripts"></p> 

* Shell脚本

    * Shell脚本

        * 脚本格式

            ```
            #!/bin/bash
            ```

        * 创建一个脚本

            ```
            mkdir scripts
            cd scripts
            touch hello.sh
            vim hello.sh
            添加如下内容
            #!/bin/bash
            echo "hello world"
            通过bash或者是sh来执行脚本
            bash/sh hello.sh
            通过路径直接来执行脚本(前提：需要开放执行权限 chmod u+x 文件)
            通过source来执行脚本 来源于cshell
            source hello.sh
            通过. 命令执行 .本质上是bashshell
            bash,sh,路径都是在bash内部创建子shell来执行脚本
            source, . 不需要bash嵌套直接生效
            ```

        * 变量

            * 系统环境变量($HOME,$SHELL...)

                * 查看所有全局变量

                    ```
                    env / printenv
                    ```

                * 查看某个全局变量

                    ```
                    echo $变量名
                    printenv 全局变量名
                    ```

                * 判断是否为全局变量

                    ```
                    bash创建一个子bash 判断是否可以查看外部变量
                    ```

                * 查看所有变量

                    ```
                    set
                    ```

                * 输入执行自定义脚本

                    ```
                    echo $PATH
                    将脚本放到如下路径下即可执行
                    ```

                    

            * 自定义变量

                * 基本使用

                    ```
                    定义一个a变量
                    a=1
                    打印该变量
                    echo $a
                    ```

                * 将创建出来的局部变量提升为全局

                    ```
                    由于我们在子shell里面拿不到自定义变量所以来到shell
                    export 自己定义的变量
                    ```

                * 注意事项

                    * 在子shell里面讲变量进行修改返回父shell是监测不到的,但是反过来是行的
                    * echo定义的变量是类型是字符串如果想要添加计算属性$[] / $(())
                    * 定义变量的时候不能包含空格
                    * 定义变量名不能以数字开头

                * 创建只读变量

                    ```
                    readonly a=2
                    ```

                * 撤销变量

                    ```
                    unset 变量名
                    //只读变量不能撤销
                    ```

                * 特殊变量

                    * 语法

                        ```
                        echo $0 //代表脚本的名称
                        echo $1-9 //代表脚本传入的参数
                        echo {10} //当传入参数大于10个需要使用花括号
                        ```

                    * 使用

                        ```
                        echo $1 //代表输入的第一个参数
                        echo $# //统计输入参数的个数
                        echo $* //查看参数
                        echo $@ //将参数以数组的形式进行包装
                        echo $? //返回最后一次命令的状态 0代表正常
                        ```

                * 运算符

                    * 语法结构

                        ```
                        expr 参数一 参数二 参数三
                        echo $[1+2] 
                        ```

                    * 赋值操作

                        ```
                        a=$(expr 2 + 4)
                        a=$((1+3)) / a=$[1+2]
                        ```

                * 条件判断

                    * 基本条件判断

                        ```
                        test $a = hello // [ $a = hello ]
                        echo $?
                        如果[]中间没有空格 那么返回结果永远都是0，如果里面有空格且为空值，返回结果为1
                        ```

                    * 大小判断

                        ```
                        -lt 小于
                        -gt 大于
                        -eq 等于
                        -ne 不等于
                        -le 小于等于
                        -ge 大于等于
                        ```

                    * 判断权限

                        ```
                        [ -r/w/x 文件名]
                        echo $? 
                        ```

                    * 判断文件类型

                        ```
                        [ -e /home/satrol/info ] //判断文件是否存在
                        [ -f 文件 ] //判断是否是一个文件 
                        [ -d 文件 ] //判断是否是一个目录
                        ```

                    * 逻辑运算符

                        ```
                        与三目操作符相似 
                        [ hello ] && echo OK || echo Error
                        ```

                * if条件分支语句

                    * 单分支

                        * 语法

                            ```
                            if [ 条件判断语句 ]; then echo "正确返回的结果"; fi
                            ```

                        * 结合逻辑判断

                            ```
                            if [ $a -lt 20 ] && [ $a -gt 17 ]; then echo "congratulation"; fi
                            如果想要将两个数组合并
                            if [ $a -lt 20 -a $a -gt 17 ]; then echo "congratulation"; fi
                            ```

                    * 双分支

                        ```
                        if [ $2 -lt 18 ];
                        then echo "未成年";
                        else echo "成年";
                        fi
                        ```

                    * 多分支

                        ```
                        if [ $3 -lt 18 ];
                        then echo "未成年";
                        elif [ $3 -lt 40 ];
                        then echo "中年人";
                        else echo "老年人";
                        fi
                        ```

                        

                * case分支语句

                    ```
                    case $1 in 
                    1)
                    	echo "first"
                    ;;
                    2)
                    	echo "second"
                    ;;
                    3)
                    	echo "thrid"
                    ;;
                    *)
                    	echo "other"
                    ;;
                    esac
                    ```

                    

                * for循环

                    * 第一种写法

                        ```
                        //在双小括号里面可以书写运算符号
                        for(( i=1; i<=$1; i++ ))
                        do
                        	sum=$[$sum+$i];
                        done
                        	echo $sum;
                        ```

                    * 第二种写法

                        ```
                        for os in Linux windows macos;do echo $os;done
                        //两种写法结合
                        for i in {1..100}; do sum=$[$sum+$i]; done; echo $sum
                        ```

                    * $@ 和$*区别

                        ```
                        echo '========$*======'
                        for param in "$*"
                        do
                                echo $param
                        done
                        //返回结果一行显示
                        echo '=======$@======='
                        for parm in "$@"
                        do
                                echo $parm
                        done
                        //显示结果多行显示
                        ```

                        

                * while循环

                    * 示范

                        ```
                        a=1
                        while (($a<=$1))
                        do
                                # sum2=$[$sum2+$a];
                                # a=$[$a+1]
                                let sum2+=a
                                let a++
                        done
                                echo $sum2
                        ```

    <p id="console"></p> 

* 读取控制台输入

    * 选项

        ```
        -t 代表延迟时间
        -p 代表提示信息
        ```

    * 代码演示

        ```
        read -t 10 -p "你的姓名是"name
        echo "Hello,$name"
        ```

    <p id="function"></p> 

* 函数

    * 系统函数

        * $()命令替换

            > 对于系统函数的调用

        * basename

            ```
            basename + 路径 //返回结果为路径最后一位
            basename + 路径 + 后缀 //可以切除后缀
            ```

        * dirname

            ```
            dirname + 绝对路径 //截取到的是除最后一位其余的路径
            将相对路径转化为相对路径
            echo "script path":$(cd $(dirname $0);pwd)
            ```

            

            

        * 自定义函数

            * 简单的加法运算

                ```
                function add(){
                        s=$[ $1+$2 ]
                        echo "和为:"$s
                        return $s //return
                      	return返回的结果必须是数字
                }
                read -p "第一个参数为:" a
                read -p "第一个参数为:" b
                
                add $a $b
                echo "和: $?"
                return返回的值是在0-255范围内的
                ```

            * 返回值且结果不受限函数

                ```
                function add(){
                        s=$[ $1+$2 ]
                        echo $s
                }
                
                read -p "第一个参数为:" a
                read -p "第一个参数为:" b
                
                sum=$(add $a $b)
                echo "合为: $sum"
                ```

            * 归档文件

                ```
                tar -c代表归档
                tar -z代表压缩
                //归档参数必须只能为1个
                if [ $# -ne 1 ];
                then
                        echo "输入的参数个数不正确";
                        exit
                fi
                //第一个参数必须为目录
                if [ -d $1 ];
                then
                        echo;
                else
                        echo;
                        echo "输入的不是目录"
                        echo;
                fi
                
                DIR_NAME=$(basename $1);
                DIR_PATH=$(cd $(dirname $1); pwd);
                
                DATE=$(date +%y%m%d);
                
                FILE=archieve_{$DIR_NAME}_{$DATE}.tar.gz;
                DEST=/root/archieve/$FILE
                # 开始归档
                echo "开始归档....."
                
                tar -czf $DEST $DIR_PATH/$DIR_NAME
                if [ $? -eq 0 ];
                then
                        echo
                        echo "归档成功"
                        echo "归档成功的文件为$DEST"
                else
                        echo "归档失败"
                fi
                exit
                ```

    <p id="Regular-expression"></p> 

* 正则表达式

    * 特殊字符

        * ^ 以谁开头

            ```
            ^a //以a开头
            ```

        * $ 以谁为尾

            ```
            bash$ //以bash结尾
            ```

        * ^$代表空行

            ```
            cat 文件 | grep -n ^$ //查看空行位置
            ```

        * 通配符

            ```
            r..t //可以匹配到rt中间两位的数字
            r*t //可以匹配到rt中间无数个重复的字母
            .* //任意字符都可以进行匹配
            ```

        * 字符区间

            ```
            [a-z]: 匹配a-z内的单个字符
            [a-z]*: 匹配任意长度a-z内的任意字符
            ```

        * 字符转意

            ```
            cat archieve_test.sh | grep $ //由于$匹配的是结尾所以不转意会全部输出
            cat archieve_test.sh | grep '\$' //输出带有$
            ```

        * 手机号正则匹配

            ```
            echo "12256483942" | grep -E ^1[3-8][1-9]{9}$
            ```

            

            

    <p id="texthandle"></p> 

* 文本处理工具

    * 选项参数说明

        ```
        -d 按照指定分隔符分割列 
        -f 提取第几列 截取多列逗号分隔
        ```

    * 代码展示

        ```
        cut -d "分隔符" -f 第几列 文件名
        提取列数可以简写
        提取1-4列
        cat /etc/passwd | grep bash$ | cut -d "分隔符" -f 1-4 
        提取4列后
        4-
        提取4列前
        -4
        ```

    * 切割ip地址

        ```
        ifconfig ens160 | grep netmask | cut -d " " -f 10 
        ```

    * awk

        * 选项参数

            ```
            -F 分隔符 默认情况下为空格
            -v 赋值用户定义的变量
            ```

        * 代码

            ```
            使用grep + cut进行筛选
            cat /etc/passwd | grep ^root | cut -d ":" -f 7
            使用awk进行筛选
            cat /etc/passwd | awk -F ":" '/^root/ {print $7}'
            使用逗号进行分割 由于筛选列数是代码块可以使用逗号进行分割
            cat /etc/passwd | awk -F ":" '/^root/ {print $1","$7}'
            在筛选结果的最前面和最后面添加一句话
            cat /etc/passwd | awk -F ":" 'BEGIN{print "usershell"}{print $7}END{print "end of file"}'
            ```

        * 将passwd用户的id都加上1

            ```
            cat /etc/passwd | awk -F ":" '{print $3+1}'
            -v定义的值为一个变量可供后面使用
            cat /etc/passwd | awk -v i=1 -F ":" '{print $3+i}'
            ```

        * awk的内置变量

            ```
            FILENAME: 文件名
            NR: 行的个数
            NF: 切割后列的个数
            代码示范
            awk -F ":" '{print "文件名: " FILENAME " 行数: "NR " 列数: " NF}' /etc/passwd 
            awk提取空行
            ifconfig | awk '/^$/ {print NR}'
            awk截取ip地址
            ifconfig | awk '/netmask/ {print $2}'
            ```

    <p id="review"></p> 

* 巩固

    ```
    who //查看所有已登陆的用户
    mesg //查看是否打开消息功能
    who -T //查看用户是否打开消息功能
    mesg n //关闭消息功能
    mesg y //打开消息功能
    write 用户名 终端窗口号 //发送消息
    ```

