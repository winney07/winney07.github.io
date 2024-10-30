---
title: React-Native环境配置相关笔记
date: 2021-10-02 08:10:40
tags:
- React Native
categories:
- 前端开发框架
- React Native
---

### macOS环境配置

#### iOS 

参考博客：[MacOs M1安装Homebrew 在国内最简单方法](https://blog.csdn.net/sinat_38184748/article/details/114115441)——使用这个安装成功

##### 1.安装Homebrew 

------

###### 安装步骤：

M1芯片：

```
/bin/zsh -c "$(curl -fsSL https://gitee.com/huwei1024/HomebrewCN/raw/master/Homebrew.sh)"
```

报错：

```
command not found : brew
```

因为M1芯片的包安装位置不在是以前的`/usr/local/`，而是`/opt/homebrew`，所以要将配置文件里的环境变量改过来

1、首先进入根目录

```
$ cd ~
```

2、创建.zshrc文件

```
$ touch .zshrc
```

3、打开文件进行编辑

```
$ open -e .zshrc
```

4、如果有旧的环境就修改，没有就新增

```
export PATH=/opt/homebrew/bin:$PATH
export PATH=/opt/homebrew/sbin:$PATH
```

5、保存
使用`command + s`
6、生效环境变量

```
$ source .zshrc
```

7、测试

```
$ brew -v    // 显示版本，即安装成功
```

------



------

###### 本次安装参考内容：

开源安装脚本库：https://gitee.com/cunkai/HomebrewCN

复制以下内容到你的终端：
intel芯片：

```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

M1芯片：

```
/bin/zsh -c "$(curl -fsSL https://gitee.com/huwei1024/HomebrewCN/raw/master/Homebrew.sh)"
```

回车运行，按照提示运行下去就可以了

错误
做完上面的傻瓜式操作，理论上就OK了，但是我这边出现了安装完后用不了的错误

```
command not found : brew
```

------



------

###### 相关参考内容：

[Homebrew国内如何自动安装（国内地址）（Mac & Linux）](https://zhuanlan.zhihu.com/p/111014448)

旧文章：[macOS安装Homebrew太慢，换用清华镜像](https://blog.csdn.net/sinat_38184748/article/details/99450330?spm=1001.2014.3001.5502)

```
git config --global --add safe.directory /opt/homebrew/Homebrew/Library/Taps/homebrew/homebrew-core

git config --global --add safe.directory /opt/homebrew/Homebrew/Library/Taps/homebrew/homebrew-cask
```

###### 查看镜像

```
cd "$(brew --repo)" && git remote -v
```

------



#### 2.安装watchman

> 参考：[Mac系列之：Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP. Hide these hints with HOMEBREW](https://blog.csdn.net/zhengzaifeidelushang/article/details/126640559?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166458144816782417056210%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166458144816782417056210&biz_id=&utm_medium=distribute.pc_search_result.none-task-code-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-126640559-0-null-null.142^v51^control,201^v3^control_1&utm_term=Disable%20this%20behaviour%20by%20setting%20HOMEBREW_NO_INSTALL_CLEANUP.%20Hide%20these%20hints%20with%20HOMEBREW_NO_ENV_HINTS%20%28see%20%60man%20brew%60%29.)

```
brew install watchman
```

报错信息：

```
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
```

解决方法，终端输入以下命令：

```
export HOMEBREW_NO_INSTALL_CLEANUP=TRUE
```

查看版本

```
watchman -v
```



#### 3.安装cocoapods

```
brew install cocoapods
```

报错信息：

```
yarn run v1.22.19
warning ../../../../../package.json: No license field
$ react-native run-ios
info Found Xcode project "AwesomeProject.xcodeproj"
info Building (using "xcodebuild -project AwesomeProject.xcodeproj -configuration Debug -scheme AwesomeProject -destination id=A7F04948-7FA8-45D1-B4A6-C26B21B6548A")
error Failed to build iOS project. We ran "xcodebuild" command but it exited with error code 65. To debug build logs further, consider building your app with Xcode.app, by opening AwesomeProject.xcodeproj.
Command line invocation:
    /Applications/Xcode.app/Contents/Developer/usr/bin/xcodebuild -project AwesomeProject.xcodeproj -configuration Debug -scheme AwesomeProject -destination id=A7F04948-7FA8-45D1-B4A6-C26B21B6548A

User defaults from command line:
    IDEPackageSupportUseBuiltinSCM = YES

Prepare packages

Computing target dependency graph and provisioning inputs

Create build description
Build description signature: bf2f29ad51ca6266b44cbb8d643576b3
Build description path: /Users/yangyanyi/Library/Developer/Xcode/DerivedData/AwesomeProject-fgqiuteczcwroxgbdakmwcrknckt/Build/Intermediates.noindex/XCBuildData/bf2f29ad51ca6266b44cbb8d643576b3-desc.xcbuild

note: Building targets in dependency order
/Users/yangyanyi/Documents/Code/Gitee/reactive_native/AwesomeProject/ios/Pods/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject.debug.xcconfig:1:1: error: unable to open configuration settings file
/Users/yangyanyi/Documents/Code/Gitee/reactive_native/AwesomeProject/ios/Pods/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject.debug.xcconfig:1:1: error: unable to open configuration settings file
/Users/yangyanyi/Documents/Code/Gitee/reactive_native/AwesomeProject/ios/Pods/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject.debug.xcconfig:1:1: error: unable to open configuration settings file
/Users/yangyanyi/Documents/Code/Gitee/reactive_native/AwesomeProject/ios/Pods/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject.debug.xcconfig:1:1: error: unable to open configuration settings file
warning: Unable to read contents of XCFileList '/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject-resources-Debug-output-files.xcfilelist' (in target 'AwesomeProject' from project 'AwesomeProject')
warning: Unable to read contents of XCFileList '/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject-frameworks-Debug-output-files.xcfilelist' (in target 'AwesomeProject' from project 'AwesomeProject')
error: Unable to load contents of file list: '/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject-resources-Debug-input-files.xcfilelist' (in target 'AwesomeProject' from project 'AwesomeProject')
error: Unable to load contents of file list: '/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject-resources-Debug-output-files.xcfilelist' (in target 'AwesomeProject' from project 'AwesomeProject')
error: Unable to load contents of file list: '/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject-frameworks-Debug-input-files.xcfilelist' (in target 'AwesomeProject' from project 'AwesomeProject')
error: Unable to load contents of file list: '/Target Support Files/Pods-AwesomeProject/Pods-AwesomeProject-frameworks-Debug-output-files.xcfilelist' (in target 'AwesomeProject' from project 'AwesomeProject')
warning: Run script build phase '[CP] Copy Pods Resources' will be run during every build because it does not specify any outputs. To address this warning, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'AwesomeProject' from project 'AwesomeProject')
warning: Run script build phase '[CP] Embed Pods Frameworks' will be run during every build because it does not specify any outputs. To address this warning, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'AwesomeProject' from project 'AwesomeProject')
warning: Run script build phase 'Bundle React Native code and images' will be run during every build because it does not specify any outputs. To address this warning, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'AwesomeProject' from project 'AwesomeProject')
warning: Run script build phase 'Start Packager' will be run during every build because it does not specify any outputs. To address this warning, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'AwesomeProject' from project 'AwesomeProject')

** BUILD FAILED **


info Run CLI with --verbose flag for more details.
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```

解决方法：

```
cd ios 
pod install
```

> 参考：[Fresh react-native (0.66) app does not build on XCode 13, iOS 11.6: compiler error on SysUio.o]( https://lightrun.com/answers/facebook-react-native-fresh-react-native-066-app-does-not-build-on-xcode-13-ios-116-compiler-error-on-sysuioo)  
>
> 参考：[error Failed to build iOS project. We ran "xcodebuild" command but it exited with error code 65. i can not Run my Project](https://stackoverflow.com/questions/55725042/error-failed-to-build-ios-project-we-ran-xcodebuild-command-but-it-exited-wit)

报错信息：

```
[!] Error installing CocoaAsyncSocket
[!] /usr/local/bin/git clone https://github.com/robbiehanson/CocoaAsyncSocket.git /var/folders/2p/dtc9s94148j8px03g4gkxpkr0000gn/T/d20221001-8728-969mqt --template= --single-branch --depth 1 --branch 7.6.5

Cloning into '/var/folders/2p/dtc9s94148j8px03g4gkxpkr0000gn/T/d20221001-8728-969mqt'...
fatal: unable to access 'https://github.com/robbiehanson/CocoaAsyncSocket.git/': HTTP/2 stream 1 was not closed cleanly before end of the underlying stream
```

解决方法：

```
pod install
```

> 由于网络问题，不断安装中断，每次报类似的错误，继续输入pod install，就会继续安装，直到安装成功



#### 4.hermes-engine的安装问题

> 这个有490多M，每次安装都失败，报错信息都一致。这个折腾了好久好久....

报错信息：

```
[!] Error installing hermes-engine
[!] /usr/bin/curl -f -L -o /var/folders/2p/dtc9s94148j8px03g4gkxpkr0000gn/T/d20221001-67147-8lkp1c/file.tgz https://github.com/facebook/react-native/releases/download/v0.70.1/hermes-runtime-darwin-v0.70.1.tar.gz --create-dirs --netrc-optional --retry 2 -A 'CocoaPods/1.11.3 cocoapods-downloader/1.5.1'

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
  0  496M    0 1343k    0     0   1299      0   4d 15h  0:17:38   4d 14h   894
curl: (92) HTTP/2 stream 0 was not closed cleanly: PROTOCOL_ERROR (err 1)
```

解决方法：

1. 打开一个终端，先执行

```
export http_proxy='your.host:port' //your.host:port我的是127.0.0.1:1087
export https_proxy='your.host:port' your.host:port我的是127.0.0.1:1087
```

2. 这个终端界面转到项目目录下，再执行`pod install --verbose`

```
pod install --verbose						// 在安装命令添加参数`--verbose`看打印详细信息
```

> 参考：[Cocoapods安装私有库问题](https://blog.csdn.net/BUG_delete/article/details/110133505?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-110133505-blog-82894101.t0_edu_mix&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-110133505-blog-82894101.t0_edu_mix&utm_relevant_index=1)

##### 安装完成

命令行打印消息中看到自动执行`Generating Pods project`

命令行打印消息中看到自动执行`Integrating client project`

```
[!] Please close any current Xcode sessions and use `myapp.xcworkspace` for this project from now on.

Integrating target `Pods-myapp` (`myapp.xcodeproj` project)

Integrating target `Pods-myapp-myappTests` (`myapp.xcodeproj` project)
  - Running post integrate hooks
  - Writing Lockfile in `Podfile.lock`
  - Writing Manifest in `Pods/Manifest.lock`
  CDN: trunk Relative path: CocoaPods-version.yml exists! Returning local because checking is only performed in repo update

-> Pod installation complete! There are 59 dependencies from the Podfile and 49 total pods installed.
```

> 根据终端提示，如果想要使用刚添加的第三方库，必须打开`MyApp.xcworkspace`，而非之前的`MyApp.xcodeProj`。

[CocoaPods的安装与使用](https://www.jianshu.com/p/c19df91997fd)



#### 5.运行项目

```
yarn ios 
或
yarn react-native run-ios
```



#### 配置 ANDROID_SDK_ROOT 环境变量

1.打开配置文件的命令

```
vi ~/.zshrc

vi /Users/yangyanyi/.zshrc
```

2.编辑配置文件，将以下代码粘贴到配置文件中

```
# 如果你不是通过Android Studio安装的sdk，则其路径可能不同，请自行确定清楚
export ANDROID_SDK_ROOT=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_SDK_ROOT/emulator
export PATH=$PATH:$ANDROID_SDK_ROOT/tools
export PATH=$PATH:$ANDROID_SDK_ROOT/tools/bin
export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools
```

3.保存后退出vi，参考：[Mac终端编辑完成后如何保存](https://wenku.baidu.com/view/e4705173bd23482fb4daa58da0116c175f0e1e80.html)

```
:wq
```

4.使用`source $HOME/.zshrc`命令来使环境变量设置立即生效（否则重启后才生效）

```
source $HOME/.zshrc
```

5.使用`echo $ANDROID_SDK_ROOT`检查此变量是否已正确设置

```
echo $ANDROID_SDK_ROOT
```

> 输入完，在终端成功显示：`/Users/yangyanyi/Library/Android/sdk`





#### 运行项目

报错信息：

```
FAILURE: Build failed with an exception.

* What went wrong:
A problem occurred configuring project ':react-native-gradle-plugin'.
> Could not resolve all files for configuration ':react-native-gradle-plugin:classpath'.
   > Could not download kotlin-gradle-plugin-1.6.10.jar (org.jetbrains.kotlin:kotlin-gradle-plugin:1.6.10)
      > Could not get resource 'https://repo.maven.apache.org/maven2/org/jetbrains/kotlin/kotlin-gradle-plugin/1.6.10/kotlin-gradle-plugin-1.6.10.jar'.
         > Could not GET 'https://repo.maven.apache.org/maven2/org/jetbrains/kotlin/kotlin-gradle-plugin/1.6.10/kotlin-gradle-plugin-1.6.10.jar'.
            > Connect to repo.maven.apache.org:443 [repo.maven.apache.org/151.101.40.215] failed: connect timed out
   > Could not download kotlin-compiler-embeddable-1.6.10.jar (org.jetbrains.kotlin:kotlin-compiler-embeddable:1.6.10)
      > Could not get resource 'https://repo.maven.apache.org/maven2/org/jetbrains/kotlin/kotlin-compiler-embeddable/1.6.10/kotlin-compiler-embeddable-1.6.10.jar'.
         > Could not GET 'https://repo.maven.apache.org/maven2/org/jetbrains/kotlin/kotlin-compiler-embeddable/1.6.10/kotlin-compiler-embeddable-1.6.10.jar'.
            > Connect to repo.maven.apache.org:443 [repo.maven.apache.org/151.101.40.215] failed: connect timed out

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 12m 28s

error Failed to install the app. Make sure you have the Android development environment set up: https://reactnative.dev/docs/environment-setup.
Error: Command failed: ./gradlew app:installDebug -PreactNativeDevServerPort=8081

FAILURE: Build failed with an exception.

* What went wrong:
A problem occurred configuring project ':react-native-gradle-plugin'.
> Could not resolve all files for configuration ':react-native-gradle-plugin:classpath'.
   > Could not download kotlin-gradle-plugin-1.6.10.jar (org.jetbrains.kotlin:kotlin-gradle-plugin:1.6.10)
      > Could not get resource 'https://repo.maven.apache.org/maven2/org/jetbrains/kotlin/kotlin-gradle-plugin/1.6.10/kotlin-gradle-plugin-1.6.10.jar'.
         > Could not GET 'https://repo.maven.apache.org/maven2/org/jetbrains/kotlin/kotlin-gradle-plugin/1.6.10/kotlin-gradle-plugin-1.6.10.jar'.
            > Connect to repo.maven.apache.org:443 [repo.maven.apache.org/151.101.40.215] failed: connect timed out
   > Could not download kotlin-compiler-embeddable-1.6.10.jar (org.jetbrains.kotlin:kotlin-compiler-embeddable:1.6.10)
      > Could not get resource 'https://repo.maven.apache.org/maven2/org/jetbrains/kotlin/kotlin-compiler-embeddable/1.6.10/kotlin-compiler-embeddable-1.6.10.jar'.
         > Could not GET 'https://repo.maven.apache.org/maven2/org/jetbrains/kotlin/kotlin-compiler-embeddable/1.6.10/kotlin-compiler-embeddable-1.6.10.jar'.
            > Connect to repo.maven.apache.org:443 [repo.maven.apache.org/151.101.40.215] failed: connect timed out

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 12m 28s

    at makeError (/Users/yangyanyi/Documents/Code/Gitee/reactive_native/myapp/node_modules/execa/index.js:174:9)
    at /Users/yangyanyi/Documents/Code/Gitee/reactive_native/myapp/node_modules/execa/index.js:278:16
    at processTicksAndRejections (node:internal/process/task_queues:96:5)
    at async runOnAllDevices (/Users/yangyanyi/Documents/Code/Gitee/reactive_native/myapp/node_modules/@react-native-community/cli-platform-android/build/commands/runAndroid/runOnAllDevices.js:109:5)
    at async Command.handleAction (/Users/yangyanyi/Documents/Code/Gitee/reactive_native/myapp/node_modules/@react-native-community/cli/build/index.js:142:9)
info Run CLI with --verbose flag for more details.
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```

