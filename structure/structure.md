# 项目结构


`Kernel/`：（未来会有的）内核。

`Loader/`：UEFI demo

`Std/`：`C4m`标准库，包括了一些必要的高级特性和功能，如ELF装载、日志、硬件平台支持等等。

其余部分为`C4m`编译器前端。

接下来会从前端开始逐步讲解：

## 前端

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

`SumType.hs`：和类型。

`ProductType.hs`：乘积类型，可用于定义结构等等较高级的类型。

`Structure.hs`：定义了结构类型。结构类型有生命周期和作用域，可以从堆上被分配。

`Unsafe.hs`：定义了`Unsafe`操作。

`IR.hs`：用于生成我们自定义的中间表示。

## 标准库

`Basic.hs`：

`Box.hs`：

`ELF.hs`：用于支持ELF文件的装载。

`Iteratee.hs`：用于编译期循环。

`Log.hs`：一个简单的Logger，支持输出字符串、字符串字面量、十六进制数和十进制数。

`StringLiteral.hs`：字符串字面量。

`Option.hs`：TBD

`Vec.hs`：

`X86_64.hs`：平台支持。

## Demo

（并不多）
