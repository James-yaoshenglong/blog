---
title: 2021 Week8 Notes
date: 2022-02-23 21:37:49
categories:
- Weekly Notes
tags:
- Weekly Notes
---

windows docker机器学习：

1. 升级到21H2或win11
2. 安装对应的nVidia显卡驱动
3. 直接使用docker desktop

docker使用的几个注意实现

docker create 是从镜像create一个容器，要有对应的命令，不然启动不了

docker run是从镜像直接run一个容器，执行对应的命令

使用`-v`选项挂载宿主机目录，docker中间的目录会自动创建

在docker中间使用jupyter的时候要是定ip和端口，不然在宿主机上无法访问

```
jupyter notebook --notebook-dir=/opt/notebooks --ip='0.0.0.0' --port=8888 --no-browser --allow-root
```



解决gdb和实际shell运行地址不一致问题

1. 使用core dump file

   ```
   ulimit -c unlimited
   ```

2. 使用env，感觉不怎么起作用

   https://www.cnblogs.com/yhjoker/p/9161716.html

默认gdb也可以显示各种界面

```
dashboard -layout source assembly registers stack
```

