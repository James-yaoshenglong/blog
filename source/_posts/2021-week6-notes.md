---
title: 2021 Week6 Notes
date: 2022-02-09 20:13:22
categories:
- Weekly Notes
tags:
- Weekly Notes
---

linux 可以使用history命令查看历史命令记录

Linux可以使用cmp命令查看两个binary文件不同的byte

使用`-l`选项时第一个列表示编号，时十进制，第二三列表示对应的bytes，是八进制



linux创建制定大小全`0`文件

```
dd if=/dev/zero of=upload_test bs=file_size count=1
```

https://stackoverflow.com/questions/139261/how-to-create-a-file-with-a-given-size-in-linux

linux修改某个文件从某个byte开始的几个位置

```
printf '\x31\xc0\xc3' | dd of=test_blob bs=1 seek=100 count=3 conv=notrunc 
```

https://stackoverflow.com/questions/4783657/write-byte-at-address-hexedit-modify-binary-from-the-command-line

