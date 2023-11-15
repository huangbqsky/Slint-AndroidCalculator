# Slint-AndroidCalcualator


Slint 1.3 增加了对 Android app 的支持，本篇文章将通过一个简单的案例 —— 计算器，来探讨下如果目前采用 Slint 编写 Android 是否可用于生产

## 准备工具链
如果要编译 Android 项目，还需要一些简单的配置：

1.安装 Android SDK 和 Android NDK

2.配置 Android SDK 和 Android NDK 环境变量

3.安装安卓构建工具

4.安装 cargo-apk


## 新建计算器项目
要创建 Android 应用，需要新建 lib 项目， crate 必须是具有 crate-type 的 cdylib 库。另外，我们还需要借助 i-slint-backend-android-activity 这个 crate。详细配置如下：
```
[package]
name = "calculator-rs"
version = "0.1.0"
edition = "2021"

[lib]
crate-type = ["cdylib"]

[dependencies]
slint = "1.3.0"
i-slint-backend-android-activity = { version = "=1.3.0", features = ["native-activity"] }
```

## 测试计算器项目

运行如下命令，生成apk包：
```
cargo apk run --target aarch64-linux-android --lib
```
