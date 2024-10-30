---
title: JavaScript生成随机密码
date: 2020-05-21 15:12:23
tags:
- JavaScript
categories: 
- JavaScript
---

### 生成一个长度为N位的随机密码

方法一：

```
function generateRandomPassword(length) {
  const charset = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
  let password = '';
  
  for (let i = 0; i < length; i++) {
    const randomIndex = Math.floor(Math.random() * charset.length);
    password += charset[randomIndex];
  }
  
  return password;
}

const randomPassword = generateRandomPassword(10); // 生成一个10位的随机密码
console.log(randomPassword); // 打印随机生成的密码
```

方法二：

```
function generateRandomPassword(length) {
  const chars = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
  let password = '';

  for (let i = 0; i < length; i++) {
    const charType = Math.floor(Math.random() * 3); // 0: 数字, 1: 大写字母, 2: 小写字母
    let randomChar = '';

    if (charType === 0) {
      randomChar = String.fromCharCode(Math.floor(Math.random() * 10) + 48); // 48-57 是数字的 Unicode 范围
    } else if (charType === 1) {
      randomChar = String.fromCharCode(Math.floor(Math.random() * 26) + 65); // 65-90 是大写字母的 Unicode 范围
    } else if (charType === 2) {
      randomChar = String.fromCharCode(Math.floor(Math.random() * 26) + 97); // 97-122 是小写字母的 Unicode 范围
    }

    password += randomChar;
  }

  return password;
}

const randomPassword = generateRandomPassword(10); // 生成一个10位的随机密码
console.log(randomPassword); // 打印随机生成的密码
```

方法三：

```
function getRandom(min, max) {
    return Math.round(Math.random() * (max - min) + min);
}

function getCode(length) {
    let code = '';
    for (var i = 0; i < length; i++) {
        var type = getRandom(1, 3);
        switch (type) {
            case 1:
                code += String.fromCharCode(getRandom(48, 57));//数字
                break;
            case 2:
                code += String.fromCharCode(getRandom(97, 122));//小写字母
                break;
            case 3:
                code += String.fromCharCode(getRandom(65, 90));//大写字母
                break;
        }
    }
    return code;
}

var randomPassword = getCode(15);
```

> 根据自己喜欢的风格，选其一就好