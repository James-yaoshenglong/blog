---
title: 2021 Week4 Notes
date: 2022-01-25 00:37:41
categories:
- Weekly Notes
tags:
- Weekly Notes
---



# llvm学习

load pass in clang

leagcy mode:

in source code

```
//-----------------------------------------------------------------------------
// Legacy PM Registration
//-----------------------------------------------------------------------------
// The address of this variable is used to uniquely identify the pass. The
// actual value doesn't matter.
char LegacyHelloWorld::ID = 0;

// This is the core interface for pass plugins. It guarantees that 'opt' will
// recognize LegacyHelloWorld when added to the pass pipeline on the command
// line, i.e.  via '--legacy-hello-world'
static RegisterPass<LegacyHelloWorld>
    X("legacy-hello-world", "Hello World Pass",
      true, // This pass doesn't modify the CFG => true
      false // This pass is not a pure analysis pass => false
    );

//register pass to clang
static void registerMyPass(const PassManagerBuilder &,
                           llvm::legacy::PassManagerBase &PM) {
    PM.add(new LegacyHelloWorld()); // PM 用于添加 Pass
}
static RegisterStandardPasses
    RegisterMyPass(PassManagerBuilder::EP_EarlyAsPossible,
                   registerMyPass);
```

usage in command line

```
clang -Xclang -load -Xclang ../BlockMatch/build/libHelloWorld.so test.c insert.c
```

new pass manager

no idea now, may be work in llvm and clang 13

usage in command line

```
clang -fpass-plugin=libMyPass.so file.cpp
```



使用wrapper解决了clang使用pass, `-load`参数被误解的问题

[LLVM Pass入门导引](https://zhuanlan.zhihu.com/p/122522485)



# CTF

chunk extend

[chunk extend](https://nightrainy.github.io/2019/07/25/chunk-extend-and-overlapping/)

后向合并

就是通过修改chunk的size导致chunk的size的变大然后先后合并，这样重新分配出来就获得一个更长的区块，然后对中间free的部分做修改即可进行诸如fast bin attack之类的攻击

前向合并则是通过修改pre_inuse和pre_size来通过unlink的时候和前面进行合并



# Linux

云服务器虚拟机除了设置的网络组的安全权限以外，如不能访问，还要注意本机防火墙iptables的配置，具体开关及配置方法参考网络博客



`make -j`参数表示可以进行多线程编译



静态库编译先编译成`xxx.o`文件，然后再用`ar -r libxxx.a xxx.o`编译成静态库

链接的时候要放在编译命令的结尾处

https://blog.csdn.net/x_studying/article/details/53561101



clangd配置在任何环境下使用`bear compilecommand`即可完成配置
