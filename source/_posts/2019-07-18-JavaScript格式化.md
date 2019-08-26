---
title: JavaScript格式化
date: 2019-07-18 20:30:10
categories:
- 光鲜的前端
- JavaScript
tags:
- js格式化
---
本博客收集了很多JS对格式的处理，以待使用时查阅。
<!--more-->

- 金额格式化
```javascript
export function amountFormatter(amount, keyType) {
    // console.log("str:", amount)
    //金额转换:小数位不做处理，并每隔3位用逗号分开 1,234.56
    //let amountStr = (amount / 100).toFixed(2) + ''
    //取到整数部分
    if (typeof amount == "undefined" || amount == null || amount == "") {
        return ''
    } else {
        let amountStr = String(amount)
        if (amountStr.indexOf(".") > 0) {
            let intSum = amountStr.substring(0, amountStr.indexOf(".")).replace(/\B(?=(?:\d{3})+$)/g, ',')
            //取到小数部分搜索
            let dot = amountStr.substring(amountStr.indexOf("."), amountStr.length)
            if (keyType && keyType.split("-").length > 1) {
                let dotSize = parseInt(keyType.split("-")[1]) + 1
                //console.log(keyType, "keyType", dotSize)
                dot = dot.substring(0, dotSize)
                while (dot.length < dotSize) {
                    dot += '0'
                }
            }
            if (dot == ".") {
                dot = ".00"
            }
            let ret = intSum + dot;
            return ret;
        } else {
            let intSum = amountStr.replace(/\B(?=(?:\d{3})+$)/g, ',')
            let dot = ""
            if (keyType && keyType.split("-").length > 1) {
                dot = "."
                let dotSize = parseInt(keyType.split("-")[1]) + 1
                while (dot.length < dotSize) {
                    dot += '0'
                }
            }
            if (dot == ".") {
                dot = ".00"
            }
            let ret = intSum + dot;
            return ret
        }
    }
}
```
- 限制只能输入数字
包括正负数，小数
```javascript
onkeypress="return(/(\-|[0-9]|\.)/.test(String.fromCharCode(event.keyCode)))"
```
- 获取随机数
```javascript
export function getRandom(length) {
    if (!length) {
        length = 6
    }
    let random = ""
    for (let i = 0; i < length; i++) {
        const a = Math.floor(Math.random() * 10)
        console.log("==============>", a)
        random += a
    }
    //console.log("==============>", random)
    return random
}
```
} else {
            let intSum = amountStr.replace(/\B(?=(?:\d{3})+$)/g, ',')
            let dot = ""
            if (keyType && keyType.split("-").length > 1) {
                dot = "."
                let dotSize = parseInt(keyType.split("-")[1]) + 1
                while (dot.length < dotSize) {
                    dot += '0'
                }
            }
            if (dot == ".") {
                dot = ".00"
            }
            let ret = intSum + dot;
            return ret
        }
    }
}
```
- 限制只能输入数字
包括正负数，小数
```javascript
onkeypress="return(/(\-|[0-9]|\.)/.test(String.fromCharCode(event.keyCode)))"
