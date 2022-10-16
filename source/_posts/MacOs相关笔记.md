---
title: MacOs相关笔记
date: 2021-10-01 06:59:49
tags:
- Mac
---

#### Mac系统——iOS环境



##### 安装Homebrew 

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

经过检查后发现，是因为M1芯片的包安装位置不在是以前的`/usr/local/`
而是`/opt/homebrew`，所以要将配置文件里的环境变量改过来

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
$ brew -v
```


原文链接：[MacOs M1安装Homebrew 在国内最简单方法](https://blog.csdn.net/sinat_38184748/article/details/114115441)——使用这个安装成功



[Homebrew国内如何自动安装（国内地址）（Mac & Linux）](https://zhuanlan.zhihu.com/p/111014448)

旧文章：[macOS安装Homebrew太慢，换用清华镜像](https://blog.csdn.net/sinat_38184748/article/details/99450330?spm=1001.2014.3001.5502)



```
git config --global --add safe.directory /opt/homebrew/Homebrew/Library/Taps/homebrew/homebrew-core

git config --global --add safe.directory /opt/homebrew/Homebrew/Library/Taps/homebrew/homebrew-cask
```


##### 查看镜像

```
cd "$(brew --repo)" && git remote -v
```





#### 安装watchman

```
brew install watchman
```

##### 报错信息

```
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
```

解决：

```
export HOMEBREW_NO_INSTALL_CLEANUP=TRUE
```

参考：[Mac系列之：Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP. Hide these hints with HOMEBREW](https://blog.csdn.net/zhengzaifeidelushang/article/details/126640559?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166458144816782417056210%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166458144816782417056210&biz_id=&utm_medium=distribute.pc_search_result.none-task-code-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-126640559-0-null-null.142^v51^control,201^v3^control_1&utm_term=Disable%20this%20behaviour%20by%20setting%20HOMEBREW_NO_INSTALL_CLEANUP.%20Hide%20these%20hints%20with%20HOMEBREW_NO_ENV_HINTS%20%28see%20%60man%20brew%60%29.)

查看版本

```
watchman -v
```

#### 安装cocoapods

```
brew install cocoapods
```







镜像地址

```
https://mirrors.tuna.tsinghua.edu.cn
```

```
npm config set registry 镜像地址
```

```
npm ---- https://registry.npmjs.org/
cnpm --- http://r.cnpmjs.org/
taobao - https://registry.npmmirror.com
edunpm - http://registry.enpmjs.org/
eu ----- http://registry.npmjs.eu/
au ----- http://registry.npmjs.org.au/
sl ----- http://npm.strongloop.com/
nj ----- https://registry.nodejitsu.com/
pt ----- http://registry.npmjs.pt/

```





切换回淘宝镜像

```
npm config set registry https://registry.npmmirror.com/
```

先用淘宝镜像安装项目，

```
npx react-native init AwesomeProject
```

`安装不了cocoapods`

切换到`https://registry.npmmirror.com/`

切换到项目目录

```
cd AwesomeProject
```

再安装cocoapods

```
npm i cocoapods
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

参考：[Fresh react-native (0.66) app does not build on XCode 13, iOS 11.6: compiler error on SysUio.o]( https://lightrun.com/answers/facebook-react-native-fresh-react-native-066-app-does-not-build-on-xcode-13-ios-116-compiler-error-on-sysuioo)  

参考：[error Failed to build iOS project. We ran "xcodebuild" command but it exited with error code 65. i can not Run my Project](https://stackoverflow.com/questions/55725042/error-failed-to-build-ios-project-we-ran-xcodebuild-command-but-it-exited-wit)

原因可能是没有安装cocoapods成功

```
cd ios 
```

```
pod install
```

然后报错信息：

```
[!] Error installing CocoaAsyncSocket
[!] /usr/local/bin/git clone https://github.com/robbiehanson/CocoaAsyncSocket.git /var/folders/2p/dtc9s94148j8px03g4gkxpkr0000gn/T/d20221001-8728-969mqt --template= --single-branch --depth 1 --branch 7.6.5

Cloning into '/var/folders/2p/dtc9s94148j8px03g4gkxpkr0000gn/T/d20221001-8728-969mqt'...
fatal: unable to access 'https://github.com/robbiehanson/CocoaAsyncSocket.git/': HTTP/2 stream 1 was not closed cleanly before end of the underlying stream
```

解决：

(可能也不需要做下面这个设置，每次报以上错误的时候，一直pod install，直到安装成功)

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

参考：[SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443](https://stackoverflow.com/questions/48987512/ssl-connect-ssl-error-syscall-in-connection-to-github-com443)



#### hermes-engine的安装问题

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

> 这个问题折腾了好久好久好久好久......

##### 解决方案：

1. 打开一个终端，先执行

```
export http_proxy='your.host:port' //your.host:port我的是127.0.0.1:1087
export https_proxy='your.host:port' your.host:port我的是127.0.0.1:1087
```

2. 这个终端界面转到项目目录下，再执行pod install --verbose

```
pod install --verbose
```

> 在安装命令添加参数`--verbose`看打印详细信息

参考：[Cocoapods安装私有库问题](https://blog.csdn.net/BUG_delete/article/details/110133505?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-110133505-blog-82894101.t0_edu_mix&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-110133505-blog-82894101.t0_edu_mix&utm_relevant_index=1)



##### 安装完成

然后自动执行`Generating Pods project`

然后自动执行`Integrating client project`

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

##### 运行项目

```
yarn ios 
或
yarn react-native run-ios
```





```
echo insecure >> ~/.curlrc然后 pod install
```

```
解决办法：
1.删除项目依赖包以及 yarn 缓存
rm -rf node_modules && yarn cache clean
2.重新装包
yarn install
3.清除 React-Native 缓存
rm -rf ~/.rncache
```



如果iOS使用的是Mac M1的架构，可能还会遇到Cocoapods 的一些兼容问题。如果在安装 pods依赖时出现问题，可以尝试运行下面的命令：

```
sudo arch -x86_64 gem install ffi
arch -x86_64 pod install
```

[详解React Native项目中启用Hermes引擎](https://www.jb51.net/article/263303.htm)

[解决 React-Native mac 运行报错 error Failed to build iOS project. We ran "xcodebuild" command but it exite](https://blog.csdn.net/u010208471/article/details/92068560)

[s](https://developer.apple.com/forums/thread/682927)

[更新到最新版本RN 0.64.0后，React本机应用程序将无法运行](https://cloud.tencent.com/developer/ask/sof/514376)

[Installing React Native with Mapbox Navigation in iOS](https://medium.com/alameda-dev/installing-react-native-mapbox-navigation-in-ios-e35d43c5987a)

参考：[[!] Error installing Fabric. /usr/bin/curl -f -L -o /var/folders](https://blog.csdn.net/LIUXIAOXIAOBO/article/details/82894101)

参考：[【解决】[!] Error installing Fabric. [!]/usr/bin/curl -f -L -o /var/folders](https://www.jianshu.com/p/b079d6566c67)

[Pod Error installing Bugly](https://blog.csdn.net/u012477117/article/details/122241972)

[pod install 报错 :error installing AMapFoundation ,iOS 大佬们来看一下](http://www.caotama.com/670255.html)

[Failed to build iOS project. We ran "xcodebuild" command but it exited with error code 65](https://stackoverflow.com/questions/65458086/failed-to-build-ios-project-we-ran-xcodebuild-command-but-it-exited-with-erro)

[镜像切换](https://blog.csdn.net/qingpingguo12/article/details/126137315)



[Mac全自动安装brew一键配置国内镜像源](https://blog.csdn.net/CaptainJava/article/details/109132783)

[Mac HomeBrew国内镜像安装方法](https://blog.csdn.net/hh680821/article/details/104936180?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166457782716782417034485%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166457782716782417034485&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-104936180-null-null.142^v51^control,201^v3^control_1&utm_term=homebrew%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F%E5%AE%89%E8%A3%85&spm=1018.2226.3001.4187)







[科学上网](https://github.com/yanue/V2rayU/releases/tag/3.3.0)



淘宝镜像：https://mirrors.aliyun.com/homebrew/?spm=a2c6h.13651104.0.0.1fc17608pdL2JD









#### [Mac系统下——Android 环境](https://www.reactnative.cn/docs/environment-setup)

Java Development Kit

```
brew tap homebrew/cask-versions
brew install --cask zulu11
```

React Native 需要 Java Development Kit [JDK] 11。你可以在命令行中输入 `javac -version`（请注意是 javac，不是 java）来查看你当前安装的 JDK 版本



##### 3. 配置 ANDROID_SDK_ROOT 环境变量[](https://www.reactnative.cn/docs/environment-setup#3-配置-android_sdk_root-环境变量)

React Native 需要通过环境变量来了解你的 Android SDK 装在什么路径，从而正常进行编译。

具体的做法是把下面的命令加入到 shell 的配置文件中。如果你的 shell 是 zsh，则配置文件为`~/.zshrc`，如果是 bash 则为`~/.bash_profile`（可以使用`echo $0`命令查看你所使用的 shell。）：

```shell
# 如果你不是通过Android Studio安装的sdk，则其路径可能不同，请自行确定清楚
export ANDROID_SDK_ROOT=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_SDK_ROOT/emulator
export PATH=$PATH:$ANDROID_SDK_ROOT/tools
export PATH=$PATH:$ANDROID_SDK_ROOT/tools/bin
export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools
```



> 译注：~表示用户目录，即`/Users/你的用户名/`，而小数点开头的文件在 Finder 中是隐藏的，并且这个文件有可能并不存在。可在终端下使用`vi ~/.zshrc`命令创建或编辑。如不熟悉 vi 操作，请点击[这里](http://www.eepw.com.cn/article/48018.htm)学习。

使用`source $HOME/.zshrc`命令来使环境变量设置立即生效（否则重启后才生效）。可以使用`echo $ANDROID_SDK_ROOT`检查此变量是否已正确设置。

> 请确保你正确指定了 Android SDK 路径。你可以在 Android Studio 的"Preferences"菜单中查看 SDK 的真实路径，具体是**Appearance & Behavior** → **System Settings** → **Android SDK**。
