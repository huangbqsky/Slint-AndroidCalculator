# Slint-AndroidCalculator


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

与使用任何应用程序一样android-activity，您需要将android_init函数实现为#[no_mangle]. 在其中创建一个 [ AndroidPlatform] 并将其传递给 [ slint::platform::set_platform][i_slint_core::platform::set_platform]。

## 构建和部署项目
要构建和部署应用程序，我们建议使用Cargo-apk，这是一个Cargo子命令，可构建、签名和部署用Rust制作的Android APK。

您可以通过以下命令安装并使用它：
```
cargo install cargo-apk
cargo apk run --target aarch64-linux-android --lib
```
PS：请确保已在开发环境中安装并正确设置了 Android NDK 和 SDK，以便上述命令能够按预期工作。

## 参考文档
Slint android-activity 文档：https://github.com/slint-ui/slint/tree/master/internal/backends/android-activity
