# Document for Typekernel (draft)

## 引言

`Typekernel`是一个操作系统内核项目，
目的是尝试创造一门操作系统专用语言，并用这门语言实现一个操作系统。

当下，这个目标还只实现了第一步。首先，我们选出了C语言的一个子集，
`C----`（简写为`C4m`）作为现在的目标语言。为了方便后续语言特性
的增减，并且考虑到类型安全等种种因素，我们采用`Haskell`作为`C4m`
编译器前端的实现语言。我们已经实现了`C4m`的C前端<del>和`llvm`
前端</del>。最后，我们用`C4m`实现了一个在`UEFI`上可运行的demo。

## 如何开始

本项目使用了[`Haskell Stack`](https://docs.haskellstack.org/en/stable/README/)
进行组织，如何安装可以参考[这一节](https://docs.haskellstack.org/en/stable/README/#how-to-install)，
这里提供的是*nix系统的安装方式。

```
$ curl -sSL https://get.haskellstack.org/ | sh
$ stack --version
```

一键安装。本项目亦推荐在*nix系统下进行。

`stack`准备完毕之后，在项目根目录下执行`make`即可。

## 当前问题

运行`make img`时会发生如下错误：
```
********************************
Typekernel Code Generator
********************************
Generating target/bootloader.c
typekernel-exe: src/Typekernel/Loader/UEFI.hs:47:14-26: No instance nor default method for class operation logString
```