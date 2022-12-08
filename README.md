
开发版本

step 1:

`rustup override add nightly` 来选择使用nightly版本的Rust



step 2:

根目录创建一个 `json` 文件 取名为 `x86_64-blog_os.json`

内容为：

```json
{
  "llvm-target": "x86_64-unknown-none",
  "data-layout": "e-m:e-i64:64-f80:128-n8:16:32:64-S128",
  "arch": "x86_64",
  "target-endian": "little",
  "target-pointer-width": "64",
  "target-c-int-width": "32",
  "os": "none",
  "executables": true,
  "linker-flavor": "ld.lld",
  "linker": "rust-lld",
  "panic-strategy": "abort",
  "disable-redzone": true,
  "features": "-mmx,-sse,+soft-float"
}
```



step 3:

安装 xbuild  

```bash
cargo install cargo-xbuild
```



step 4: 

安装 Rust 源代码

```bash
rustup component add rust-src
```



step 5:

安装bootimage工具

```bash
cargo install bootimage --version "^0.7.3"
```



step 6:

安装运行 bootimage 以及编译引导程序

```bash
rustup component add llvm-tools-preview
```



step 7:

运行简单程序

```bash
cargo bootimage

# 在QEMU启动内核
# 进入target里面的  bin同级目录  执行命令
qemu-system-x86_64 -drive format=raw,file=bootimage-blog_os.bin
```





可以使用`cargo xrun`来编译内核并在QEMU中启动



### 问题汇总

`0x20...0x7e`  改成   `0x20..=0x7e`


use of undeclared crate or module `fmt`

加一行  use core::fmt;
`0x20...0x7e`  改成   `0x20..=0x7e`

```toml
[dependencies]
spin = "0.4.9"
改成
spin = "0.9.4"
```

