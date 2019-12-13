# Document for Typekernel

## (draft)

### Def. 

参见 Typekernel Proposal.

### 工程结构

`Std/`：一些必要的高级特性和功能，如ELF装载、日志、硬件平台支持等等。

`Loader/`：UEFI demo，在UEFI环境下启动并输出字符串。

`Kernel/`：TBD。

`C4mAST.hs`： 当前的主定义文件，C4m → 中间表示码。

`LegacyTranspiler.hs`：先前的主定义文件，C4m → C。

`Nat.hs`： 一个自然数系统，供编译期使用。

`Memory.hs`：定义了基本类型的内存布局，利用先前定义的自然数系统对内存布局进行了编译期检查。如：

```haskell
    unsafeDword :: (KnownNat m, PeanoMod8 m Z, MonadC env)=>Proxy (m::Nat)->MLens env (Memory n) UInt64
    dword :: (KnownNat m, PeanoLT (S (S (S (S (S (S (S m))))))) n True, PeanoMod8 m Z, MonadC env)=>
        Proxy (m::Nat)->MLens env (Memory n) UInt64
```
前者为`Unsafe`，因此只需要访存地址`m`是8字节对齐的就可以了。而后者是`Safe`，因此额外
要求了访存的这8个字节在内存环境的范围之内。

除此之外，还定义了各个类型的`getter`和`setter`。这一部分是借助`MLens`完成的。

`Structure.hs`：定义了结构类型。结构类型有生命周期和作用域，可以从堆上被分配。

（TBD）

### How To Use It?

（TBD）