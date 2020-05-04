---
categories:
 - Linux
date: 2020-04-27
description: Linux 计划任务
tags:
 - Linux
 - crontab
title: "Linux 计划任务"
url: /linux/linux_crontab/
---
> 计划任务就是定时去做某些事情  
> Linux提供两种计划任务 at 和 cron  
> at 仅执行一次就结束  
> cron 循环执行  
---
> ## **at**  
> Centos 默认开启了 atd 这个服务，其他系统可自行检查 (服务相关可见http://fancygo.cn/linux/linux_systemctl/)  
> 1. 设置用户权限  
> >  优先寻找 /etc/at.allow， 写在该文件中的用户才能使用 at  
> >  然后寻找 /etc/at.deny， 写在该文件中的用户不能使用 at  
> >  若这两个文件都不存在，则只有 root 用户能使用 at  
> >  at.allow 优先级大于 at.deny  
> 2. at [time]，time格式如下
> > ```
> > HH:MM 在今天的HH:MM时刻执行，若时刻已经超过则明天该时刻执行，ex：04:00
> > HH:MM YYYY-MM-DD 在具体的时刻执行，ex：04:00 2020-4-30
> > now+ [number][minutes|hours|days|weeks]，以当前时间为基点往后多久执行，ex：now+1minutes
> > ```
> 3. 例子：
> > ```
> > at now+1minutes
> > ```
> > 该命令会打开一个shell，然后你可以输入命令，最好使用绝对路径来执行命令  
> > ```
> > ls > test
> > ```
> > 命令输完 ctrl+d 退出，然后等待执行，时间到了会把 ls 执行的结果重定向到 test 文件中  
> > 在等待过程中你可以在目下 /var/spool/at 下查看还没到时间的各个执行脚本  
> 4. atq 查询当前有哪些等待执行的任务，显示如下
> > ```
> > 6   Mon Apr 27 15:02:00 2020 a root
> > ```
> > 任务号6，后面是时间，root表示是哪个用户执行的
> 5. atrm [num]，删除任务号是 num 的任务
---
> ## **crontab**  
> Linux系统默认都开启了该服务，Centos是 crond.service，树莓派是 cron.service
> 1. 设置用户权限
> > 和at使用方法类似，cron也通过两个文件来控制权限，分别是 cron.allow 和 cron.deny
> 2. 普通用户执行 crontab -
> > 之后会进入编辑界面，每一行就是一项任务，我们输入如下内容，该任务表示每秒钟把 date 命令内容追加到 date.cron 文件中保存
> > ```
> > */1 * * * * date >> /home/fancy/date.cron
> > ```
> > 以上编辑内容一共有6个字段，前5个字段表示时间设置，第6个字段是任务执行命令
> > 具体对应如下
> > ```
> > */1   *    *    *    *   date >> /home/fancy/date.cron
> > 分钟 小时 日期  月份  周  命令
> > * 表示任何时刻都接受，如上就是每月每日每小时的1分钟执行一次
> > , 表示分隔时段，比如日期那个字段如果是 1,2 就代表 1日和2日
> > - 表示范围，比如小时哪个字段如果是 1-2 就代表 1点到2点
> > */n 表示时间间隔，比如分钟字段如果是 */5 就代表每5分钟
> > ```
> > /var/spool/cron/[user] 文件会记录 user用户需要执行的任务
> > /var/log/cron 会记录所有任务的日志
> > crontab -l，查看cron任务列表
> > crontab -r，删除所有cron任务
> 4. 系统管理cron
> > 直接编辑 /etc/crontab 文件，默认如下格式
> > ```
> > SHELL=/bin/bash
> > PATH=/sbin:/bin:/usr/sbin:/usr/bin
> > MAILTO=root
> > For details see man 4 crontabs
> > Example of job definition:
> > .---------------- minute (0 - 59)
> > |  .------------- hour (0 - 23)
> > |  |  .---------- day of month (1 - 31)
> > |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
> > |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
> > |  |  |  |  |
> > *  *  *  *  * user-name  command to be executed
> > ```
> > 上面两行很容易理解，MAILTO是邮件地址，表示运行出错时系统发送的邮件的目的地址
> > 最下面一行的格式和 conrtab -e 编写的格式很像，但是多了一个字段
> > 第6个字段表示指定某个用户执行命令，其他的设置都一样
> > 修改完，重新启动 crond.service 即可

> ## **fancyo**  
> ## **一个例子**
---


