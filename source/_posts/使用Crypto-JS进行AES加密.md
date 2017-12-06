---
title: 使用Crypto-JS进行加密，以及使用angular的方式进行封装调用
date: 2017年1月13日10:06:51
tags: [AES,Web开发,CryptoJS]
categories: Web开发
keywords: AES加密,Crypto.js,angularjs-Crypto
description: <blockquote class="blockquote-center">由于项目需要，对于登陆接口的密码需要进行AES加密后才进行传输</blockquote>
---

<!-- more -->

<center>
## 使用Crypto-JS进行AES加密
</center>

<P>在最近的项目中，调用登录接口，需要对账号密码数据进行AES加密后再进行传输，使用的是_`AES/ECB/PKCS5Padding`_,我前端部分使用选择了_`CryptoJS`_,现在把使用的过程记录如下。

***

#### 需要注意的点
* Crypto-JS的encrypt函数不会返回字符串，需要调用对象的toString方法，或者通过Crypto-js转码才能得到真实的结果。

#### 使用步骤
1. 引入`Crypto-JS`中的 `aes.js`及相关模块
```
"bower_components/cryptojs/aes.js",
"bower_components/cryptojs/enc-utf8.js",
"bower_components/cryptojs/pad-pkcs7.js",
"bower_components/cryptojs/mode-ecb.js"
```
2. 调用CryptoJS.AES

```javascript
// 官方示例, 每次输出的密文都不一样,这样使用的话是错误的
CryptoJS.AES.encrypt("Message", "Secret Passphrase");

/* 正确的使用姿势！！ */
// 使用用户名进行MD5，32位，作为key
var key_str = md5.createHash(username);
// 将key转换成128 bit
var key = CryptoJS.enc.Utf8.parse(key_str);
// 对password进行AES加密
var AESPass = CryptoJS.AES.encrypt(password, key, {
      mode: CryptoJS.mode.ECB,  //补齐方式 CBC,ECB,etc.
      padding: CryptoJS.pad.Pkcs7 // 偏移规则设定  pack5，pkcs7，nopadding,etc.
});
// CryptoJS 的 encrypt函数不会直接返回字符串，需要toString或者Crypto-JS进行转码才能得到真实的结果。
var pass = AESPass.toString();
var authData = Base64.encode(username + ':' + pass).replace(/[\r\n]/g, ''); // 去除回车换行符
```

### 使用AngularJS的方式调用CryptoJS.AES
1. 使用Angular将`AES`封装成一个`provider`
2. 提供两种方式设置key
```javascript
// 1. 一种为在angular.module('xxxx').config中进行设置，此种方式适用于key为一个固定值的情况
	CryptoKeyProvider.setCryptofraphyKey('key') // 在config中设置key
	$crypto.encrypto('plaintext') // 在业务逻辑处直接传入需要加密的明文进行调用
// 2. 第二种方式,每次都设置不同的key
	$crypto.encrypto('plaintext','key')
```
3. 具体源码如下：
> 注意：解密时，需要先将密文转换成`Base64`的编码的格式。
> > 1. 使用`CryptoJS.enc.Hex.parse`转换成十六进制
> > 2. 使用`CryptoJS.enc.Base64.stringify`将其变成Base64编码的字符串
> > 3. 最后才能传入`CryptoJS.AES.decrypt`方法对其解密