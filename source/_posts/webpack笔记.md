---
title: webpack笔记
date: 2024-02-28 14:58:53
tags:
- webpack
---

#### 将多个js文件合并成一个js文件的同时，不进行压缩

```
const path = require("path");

module.exports = {  
  entry: "./src/wanka/index.js",  // 入口文件
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js", // 输出的文件名
  },
  mode: 'development',
  devtool: 'source-map' // 设置为生成source map
};

```



#### [import 动态导入](https://webpack.js.org/api/module-methods/#magic-comments)

根据当前渠道，打包对应的SDK

`common.js`：

```
export const pack_platform = 'hongg';   // 打包渠道名称
```

`hongg/hongg.js`：

```
export class MYWXSDK {
	
}
```

`./script/index.js`

```
import { pack_platform } from './common'

class JMMiddleSDK {
	...
	// 初始化参数
    init(initData, callback) {
    	....
    	
    	// 根据渠道，动态引入对应的SDK
    	import(/* webpackIgnore: true */`../src/${pack_platform}/${pack_platform}.js`).then(module => {
            const { MYWXSDK } = module;
            // 使用 WXSDK 进行后续操作
            console.log('MYWXSDK');
            console.log(MYWXSDK);
            this.platform = this.initData.platform;
            this.wxsdk = new MYWXSDK(init);
            this.wxsdk.init(init, callback);
          }).catch(err => {
            console.error('报错：', err);
          });
    }
```

`重点`：要在import路径参数前加`/* webpackIgnore: true */`参数，不然会遍历当前路径下的全部

`相对路径`： `../src/`， 以dist为当前路径设置的

> 每次打包前，只要修改`common.js`需要打包的渠道名称

动态导入要使用then：

```
import().then(module => {
	// module的使用
}).catch(err => {
    console.error('报错：', err);
});
```

> 以上方法存在一个问题：当渠道sdk的js文件（`hongg/hongg.js`）中有引入第三方包时，如：`import HgSdk from './HgSdk.min.js';`，则打包时第三方的代码没有被打包进去



#### 根据不同渠道，动态打包方法一

1. 渠道sdk代码

   ```
   export class MYWXSDK {
   	
   }
   ```

   > 每个渠道的class命名要一样，都是`MYWXSDK`（自定义为一样）

2. `./src/scripts/index.js`：

   ```
   import { JMSDK } from './import';
   ```

3. `package.json`

   ```
   "scripts": {
       "build": "cross-env CHANNEL=hongg webpack",
   }
   ```

   > 打包时，运行`npm run build`命令；  打包不同渠道，就将`CHANNEL的值改为对应的渠道名`

4. `webpack.config.js` ——定义环境变量 CHANNEL

   ```
   const webpack = require('webpack');
   
   module.exports = {
       // 定义环境变量 CHANNEL
       plugins: [
           new webpack.DefinePlugin({
               'process.env.CHANNEL': JSON.stringify(process.env.CHANNEL)
           })
       ],
   };
   ```

   > 使用的时：process.env.CHANNEL即可拿到CHANNEL的值

5. `webpack.config.js`——动态生成`import.js`

   ```
   const fs = require('fs');
   
   /**
    * 创建渠道importJs文件
    * @param {*} importJsPath 
    * @param {*} processEnv 
    */
   function createImportJs(importJsPath, processEnv) {
       const classPath = `../${processEnv.CHANNEL}/${processEnv.CHANNEL}.js`;
       const createImportJsContent = "import { MYWXSDK } from '" + classPath + "'; export function JMSDK(init) {return new MYWXSDK (init);}";
       
       fs.writeFile(importJsPath, createImportJsContent, 'utf8', (err) => {
           if (err) {
               console.error("import.js文件写入失败， 原因：" + err);
           } else {
               console.log('import.js文件写入成功');
           }
       });
   }
   const importJsPath = './src/scripts/import.js';
   createImportJs(importJsPath, process.env)
   ```

   在打包前，webpack入口文件index.js中引入的import.js已写入成功：

   ```
   import { MYWXSDK } from '../hongg/hongg.js'; export function JMSDK(init) {return new MYWXSDK (init);}
   ```

6. 打包命令

   ```
   npm run build
   ```

##### 优化打包方法1

1. `package.json`

   ```
   "build": "cross-env CHANNEL=$npm_config_channel webpack",
   ```

2. `webpack.config.js`

   ```
   module.exports = (env, argv) => {
       return{
           // 定义环境变量 CHANNEL————方法二
           plugins: [
               new webpack.DefinePlugin({
                    // 可以在命令行中使用 --channel 参数来指定渠道 npm run build --channel=hongg
                   'process.env.CHANNEL': JSON.stringify(argv.channel || process.env.CHANNEL)  
               })
           ],
       }
   };
   ```

3. 打包命令——直接在这里指定渠道名，不需要修改`package.json`里的build命令中的CHANNEL

   ```
    npm run build --channel=hongg
   ```

##### 优化打包方法2

> 不需要在package.json中添加命令

1. `webpack.config.js`

   ```
   // 方法二
   const webpack = require('webpack');
   const fs = require('fs');
   /**
    * 创建渠道importJs文件
    * @param {*} importJsPath 
    * @param {*} channel   渠道名称
    */
   function createImportJs(importJsPath, channel) {
       const classPath = `../${channel}/${channel}.js`;
       const createImportJsContent = "import { MYWXSDK } from '" + classPath + "'; export function JMSDK(init) {return new MYWXSDK (init);}";
   
       fs.writeFile(importJsPath, createImportJsContent, 'utf8', (err) => {
           if (err) {
               console.error("import.js文件写入失败， 原因：" + err);
           } else {
               console.log('import.js文件写入成功');
           }
       });
   }
   
   // webpakc打包配置
   module.exports = (env, argv) => {
       const importJsPath = './src/scripts/import.js';
       createImportJs(importJsPath, env.channel);
   
       return{
           // 定义环境变量 CHANNEL————方法二
           plugins: [
               new webpack.DefinePlugin({
                   // 可以在命令行中使用 --channel 参数来指定渠道  webpack --env channel=hongg
                   'process.env.CHANNEL': JSON.stringify(env.channel || process.env.CHANNEL)  
               })
           ],
       }
   };
   ```

   

#### 根据不用渠道，动态打包方法二

1. `./src/scripts/index.js`：

   ```
   import { JMSDK } from './import';
   ```

2. `script/handleSp.js`

   ```
   const fs = require('fs');
   
   module.exports = {
       /**
        * 创建渠道importJs文件
        * @param {*} importJsPath 
        * @param {*} processEnvEnviroment 
        */
       createImportJs: function (importJsPath, processEnvEnviroment) {
           const params = processEnvEnviroment.split('-');
           const className = params[0];
           const classPath = params[1];
           const createImportJsContent = "import { " + className + " } from '" + classPath + "'; export function JMSDK(init) {return new " + className + "(init);}";
   
           fs.writeFile(importJsPath, createImportJsContent, 'utf8', (err) => {
               if (err) {
                   console.error("import.js文件写入失败， 原因：" + err);
               } else {
                   console.log('import.js文件写入成功');
               }
           });
       }
   };
   ```

3. `webpack.config.js`

   ```
   // 处理自动渠道打包逻辑，生成import.js文件
   const hangleSp = require('./src/scripts/handleSp.js');
   const importJsPath = './src/scripts/import.js';
   const processEnvEnviroment = process.env.ENVIRONMENT;
   hangleSp.createImportJs(importJsPath, processEnvEnviroment);
   ```

4. `package.json`

   ```
   "scripts": {
       "zidou": "cross-env ENVIRONMENT=ZDWXSDK-../zidou/zidou npx webpack --stats-error-details",
       "feiqu": "cross-env ENVIRONMENT=FQWXSDK-../feiqu/feiqu npx webpack --stats-error-details",
       "slang": "cross-env ENVIRONMENT=SLWXSDK-../slang/slang npx webpack --stats-error-details",
       "lewan": "cross-env ENVIRONMENT=LWWXSDK-../lewan/lewan npx webpack --stats-error-details",
       "vxiny": "cross-env ENVIRONMENT=XYWXSDK-../vxiny/vxiny npx webpack --stats-error-details",
       "zhwan": "cross-env ENVIRONMENT=ZWWXSDK-../zhwan/zhwan npx webpack --stats-error-details",
    }
   ```

   > 每次新增渠道，要新增命令， 每个渠道的sdk名称可不一样

5. 打包命令

   ```
   npm run zidou		// npm run 渠道名称
   ```

   



