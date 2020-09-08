---
title: JS-reverse
date: 2020-02-07 23:29:28
tags:
- JS-reverse
categories:
- JS-reverse
keywords:
- JS-reverse
---

#### 基本格式

```js
function getpwd(plaintext){  // 一定要先找到明文
    ;
    return ciphertext  // 返回格式有两种：Hex和base64
}
```

#### 常见加密方式

```python
MD5, SHA # 不可逆 # 常用
HMAC, RC4, 
AES, DES, 3DES # 可逆 # 常用
Base64, Rabbit, PBKDF2/EvpKDF
RSA
```

#### chrome-F12

```python
search
sensors # 设置经纬度
下断点
Breakpoints # 管理断点
Call Stack # 堆栈
抓包勾选Preserve log（保存日志），页面跳转，也能保存上一个界面的日志
```

#### 工具网站

```python
http://tool.chacuo.net/cryptdes
# 用来解析公钥（RSA加密），可获取key长度，模数，指数  
# 公钥没有反斜杠'\',只有'/'
# 指数看0x，一般为0x10001,所以就是10001

# 雷电模拟器 3.63
```

#### 哈希系列通杀

```python
# CryptoJS.MD5('word')
# 哈希加密系列有一个固定值1732584193，可以直接搜索
```

#### AES加密

```python
mode # 类型，常用CBC和ECB
padding # 常用Pkos7和Iso10126
IV # 一般为固定值,要选最初值
key # 一般为固定值
# IV和key都有Eno编码规则，如UTF8
```

#### RAS加密

```python
指数:一般为10001
公钥:(很长)要找出来  # 1.上一个请求的返回值(getpublickey) 2.js文件中默认 3.js代码生成
# B64编码
# PKCS1指的每次生成值不一样
# 内容反转
# 内存反转
```

#### 技巧

```python
# 小块弹窗，右键检查源码找到目标网址，放入浏览器打开，会出现一个干净的登录界面，方便抓包
# 密码一般为哈希加密
# 遇到Encrypt加断点
# 方法有传参数，就可能是的
```

#### JS逆向工具

```python
WT-JS_DEBUG  # 找安全版本，其他的好像有病毒
```

#### JS加密实例

```python
中关村登录
pwd: 3b8aaa16fa213573513038281774d9c0  # wuyao666
# pwd : md5Password
# var md5Password = CryptoJS.MD5(password+"zol") + '';
```

```python
今目标登录
password: a2c13e941f4f68fde8d92399ddeb3bf25111a434 # wuyao666
# var result = {}
# result.password = sha1(resultData.password)
```

```python
升学e网通 # AES
password: "590d9a610747ab5392a8a164793516a8" # wuyao666
# password: i = (0, v.Encrypt)(i)
t.Encrypt = function(e) {
            var t = n["default"].enc.Utf8.parse(e);
            return n["default"].AES.encrypt(t, i, {
                iv: o,
                mode: n["default"].mode.CBC,
                padding: n["default"].pad.Pkcs7
            }).ciphertext.toString().toUpperCase()
        }
# o = n["default"].enc.Utf8.parse("2017110912453698")
```

```js
有赞 // AES # 网站已经改了
Fiddler抓包
// 对password 加密
password: d.a.encrypt(e.password)
// 源码:
n = e.enc.Utf8.parse("youzan.com.aesiv")
i = e.enc.Utf8.parse("youzan.com._key_")  # i在此处是key
var r = e.AES.encrypt(t, i, {
    mode: e.mode.CBC,
    padding: e.pad.Iso10126,
	iv: n  // 这个值很容易混淆,要找初始值，即enc.Utf8.parse()之前的值.
}).toString()
// 对ticket 加密
fingerPrint  // 指纹，其实就是加密后的一个字符串
date:{
    fingerPrint: t ? t + c.default.encrypt(r) : "",  // a?b:c
    youzanType: 2
}
// 也是AES加密
```

```python
华特东方注册加密 # 都是AES
# password 
# token
# tokens  #参数unid 
```

```python
网页百度登录加密 # RSA
# token和codestring都是可以固定值的
# gid是随机的，随机数
# password是加密了的RSA,公钥通过请求获取 # password = 
# 手机和网页端加密不一样
```

```python
手机百度登录加密 # RSA
# l.password = window.encryptedString(r,l.password)  # 前面明码经过了拼接
```

```python
运动潮流单品交易平台 # 拼接+md5
# sign 加密了
# 搜索sign
# t.data.sign || (t.data.sign = Object(I["b"])(t.data))
# t.transformRequest = M : t.params.sign = Object(I["b"])(t.params)
```

```python
# 京东登录 #RSA
# nloginpwd
```

```python
# 微博 # RSA和SHA1
sp  # e.sp = b;   # sp是密码
```

```python
# 享物说 # 滑动验证(一般都是假的,提交的请求包,没有这些参数值)
模拟器有时候会被识别为"高风险设备:伪造设备"，就不会抓到真的包，需要用自己真的手机来抓包  # fengkong
```

