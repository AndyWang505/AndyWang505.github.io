---
layout: post
title:  "[JS] 物件傳參考特性(call by reference)"
date:  2022-08-14 22:00:00 +0800
categories: JavaScript
tags: 筆記 JavaScript ByReference ShallowCopy&DeepCopy
pin: false
---
# 物件傳參考特性(call by reference)

主要想整理最近遇到的 by reference 問題，日後自己複習也能很快的了解重點和問題原因

## 物件傳參考特性

只出現在物件(Object)、陣列(Array)、函式(Function)。

假使有一個A變數的值為物件，當A變數傳值給B變數時，兩者會指向同一個記憶體位址，若嘗試更改物件內的方法或特性，也會連同更改另一個物件的方法或特性。

```javascript
const obj = {
    name: 'andy'
};
const obj2;
obj2 = obj;

console.log(obj);
console.log(obj2);
// console：
// obj = {name: 'andy'};
// obj2 = {name: 'andy'};
```
若嘗試更改 obj2 中的 name
```javascript
const obj = {
    name: 'andy'
};
const obj2;
obj2 = obj;

obj2.name = 'terry';
console.log(obj);
console.log(obj2);
// console：
// obj = {name: 'terru'};
// obj2 = {name: 'terry'};
```
則 obj 也一起被更改了
為什麼會這樣，原因是他們都是指向同一個記憶體位址，類似C語言中的指標
這邊的賦值也可以說是賦予相同的記憶體位址，這種通常稱做 call by reference，就是傳參考的意思。

![](https://i.imgur.com/iiXUSCN.png)

![](https://i.imgur.com/yh9AzBi.png)


## call by reference/call by value

call by reference 傳參考聽起來很抽象

其實每個物件都是獨立的，兩者記憶體位址不同，但當比較物件的型別時，會發現比較的是記憶體位址，並非值

也就是說大多數時候都是物件都是以傳位址的方式來進行

這裡可以再提到一個，在 JavaScript 中 Object 的定義是一對 key + value，其他則是基本型別 (Primitive type)，只有 value，就是說除了 Object 以外其他都是 call by value。

也有一派說法是說 JavaScript 只有傳值沒有傳址

以底層的角度來看只有 call by value，value 是記憶體位址，也可以說 reference 和 sharing 這種其實都是在描述行為。

不過每個人對定義的描述都不盡相同，可能就是看是怎麼解讀的吧。

## 淺層拷貝(shallow copy)/深層拷貝(deep copy)

### 解決物件傳參考的方法：

淺層拷貝(shallow copy)與深層拷貝(deep copy)

一個是共同的記憶體位址，一個是不同且各自獨立的記憶體位址

![](https://i.imgur.com/fA3LF14.png)

* ### 淺層拷貝(shallow copy)

    複製第一層的內容，但第一層內如果還有物件還是會指向同樣的記憶體位址，因此當第二層內容受到修改時，原有的物件也會受到影響

    1. Object.assign(target,source)

        將原物件配給指定物件

        ```javascript
        const person = {
            name:'andy',
            obj:{}
        }
        const person2 = Object.assign({},person);
        ```

    2. ...operator

        利用 ...array 或 ...obj 的方式達到展開效果

        ```javascript
        const person = {
            name:'andy',
            obj:{}
        }
        const person3 = {
            ...person;
        }
        ```
    
* ### 深層拷貝(deep copy)

    建立全新的物件，並完全複製整個物件包含物件中更深層的物件，兩者沒有關聯性

    1. 將 Object 轉型成 String 後再轉回 Object

        將物件轉成字串再轉成物件，確保出來的會是一個新的物件且是不同的記憶體位址。

        ```javascript
        const person = {
            name:'andy',
            obj:{}
        }
        const person2 = JSON.parse(JSON.stringify(person));
        ```

##### 參考來源

[JavaScript 淺拷貝 (Shallow Copy) 與深拷貝 (Deep Copy)](https://awdr74100.github.io/2019-10-24-javascript-deepcopy/)

[傳值(By value)與傳參考(By reference)](https://ithelp.ithome.com.tw/articles/10221006)

[[JavaScript] Javascript中的傳值 by value 與傳址 by reference](https://medium.com/itsems-frontend/javascript-pass-by-value-reference-sharing-5d6095ae030b)

[深入探討 JavaScript 中的參數傳遞：call by value 還是 reference？](https://blog.techbridge.cc/2018/06/23/javascript-call-by-value-or-reference/)

[關於JS中的淺拷貝(shallow copy)以及深拷貝(deep copy)](https://medium.com/andy-blog/%E9%97%9C%E6%96%BCjs%E4%B8%AD%E7%9A%84%E6%B7%BA%E6%8B%B7%E8%B2%9D-shallow-copy-%E4%BB%A5%E5%8F%8A%E6%B7%B1%E6%8B%B7%E8%B2%9D-deep-copy-5f5bbe96c122)

[What is the difference between a deep copy and a shallow copy?](https://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy)

[JS基本觀念：call by value 還是reference 又或是 sharing?](https://medium.com/@mengchiang000/js%E5%9F%BA%E6%9C%AC%E8%A7%80%E5%BF%B5-call-by-value-%E9%82%84%E6%98%AFreference-%E5%8F%88%E6%88%96%E6%98%AF-sharing-22a87ca478fc)

##### 以上皆為自己整理的筆記，僅供參考與複習使用。