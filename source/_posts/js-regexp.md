---
title: javascript正则
preview: 100
date: 2019-12-28 14:42:27
categories:
    - JS
    - regexp
tags:
    - Javascript
    - 正则
---
 
## 正则介绍
 
> - js里正则，主要是针对`字符串`进行的操作处理
> - js里正则有两种声明方式：通过`RegExp`和双斜杠`//`，如下
 
 
 
```javascript
/ab+c/i; // 方法一
new RegExp('ab+c', 'i'); // 方法二
new RegExp(/ab+c/, 'i'); // 方法三
```
 
 
 
## 正则规则
 
### 正则里的 修饰符（写在//右边系统定义好的规则）
 
> - `i`： 忽略大小写
> - `g`：全局匹配;找到所有匹配，而不是在第一个匹配后停止
> - `m`：允许多行匹配，如`/^abc/`匹配字符串以abc开头（忽视单行字符串，还是多行字符串），`/^abc/m`则是匹配多行字符串，每行开头的`abc`
 
------
 
### 正则里为`中括号[]`：正则里的中括号表示 `区间中的一位`
 
> - `/[2367][abcd]/`：`第一位`表示`2367之中`的某个数，`第二位`表示`abcd之中`的某个值；
> - `/[0-9][0-9A-z]/`：`第一位`表示0到9`区间中`的某个数，`第二位`表示数字或字母`区间中`的某个值
> - `/[^abdf][^1678]/`：`第一位`表示`非a或非b或非d或非f之中`的某个值，`第二位`表示`非1或非67或非7或非8之中`的某个值
> - （`注意`这里`/[^a]/`和`/^a/`的区别：中括号`里面的^a`表示`非a`，但中括号`外面的^`则是表示`以a开头`）
 
------
 
### 正则中的`小括号()`表示`子表达式`,（备注：大括号｛｝在正则里是表示量词，具体查看量词）
 
> - `/(jpg|png|gif|jpeg)/`：表示匹配`jpg`或`png`或`gif`或`jpeg`中的一个
> - `子表达式`真正厉害的作用，请查看下方正则的`复制`
> - 除了`复制`之外，小括号在正则里还可以`群组匹配`，见下方  


------
 
### 正则中的`元字符`（写在`//`中系统定义好的规则）:和`[]`一样表示`区间中的一位`
 
> - `/\w/`：`\w`其实就是系统定义好的`区间符`和`[0-9A-z_]`作用一模一样表示`0到9`及`所有字母`以及`一个下划线`之中的某一个值
> - `/\d/`：即`[0-9]`，代表数字
> - `/\s/`：空格字符，即`[\n\f\r\t\v]`匹配字符串中的这些空格符中的一个，如字符串`‘hello\nworld’`中的`\n`
> - `/\b/`：匹配单词边界，如字符串`'hello wolrd'`中`字母w`左边便有`单词边界`
> - `/\W/`或`/\D/`：`\W`即`[^\w]`；`\D`即`[^\d]`也就是`非数字`，大写均表示`非小写功能`
> - `/./`：正则里的`.`是个特殊`元字符`，表示出了`[\r\n]`之外的`所有字符中的一个`
 
------
 
### 正则中的`量词`
 
> - `+`：`1到多个`的量词，如`/a+/`,表示匹配`1到多个a`
 
 
 
```javascript
let str = 'abaaacccaa'
let reg = /a+/g
console.log(str.match(reg)) // ["a", "aaa", "aa"]
```
 
 
 
------
 
> - `*`：`0到多个`的量词，如`/a*/`,表示匹配`0到多个a`
 
 
 
```javascript
let str = 'abcabcaabccccaa'
let reg = /abc*/g
console.log(str.match(reg)) // ["abc", "abc", "abcccc"]
```
 
 
 
------
 
> - `?`：`0到一个`的量词，如`/a?/`,表示匹配`0到一个a`(注意`？`是个很特殊的`量词`，在有些情况下，它不作量词用，如`？`用在`量词后面`则表示进行`非贪婪匹配`,可以查看后面的`正则贪婪模式`介绍，再如下面的`修饰匹配`)
 
 
 
```javascript
let str = 'abaaacccaa'
let reg = /a?/g
console.log(str.match(reg)) // ["a", "", "a", "a", "a", "", "", "", "a", "a", ""]
```
 
 
 
------
 
> - `{n}`：`n个`的量词，如`/a{2}/`，表示匹配`2个a`，其作用等同于`/aa/`
 
 
 
```javascript
let str = 'abaaacccaa'
let reg = /a{2}/g
console.log(str.match(reg)) // ["aa", "aa"]
```
 
 
 
------
 
> - `{n,m}`：`n到m个`的量词，如`/a{2,4}/`，表示匹配`2到4个a`（注意，正则会优先匹配`4个a`，再匹配`3个a`，再匹配`2个a`）
 
 
 
```javascript
let str = 'abaaaaacccaaaddaa'
let reg = /a{2,4}/g
console.log(str.match(reg)) // ["aaaa", "aaa", "aa"]
```
 
 
 
------
 
> - `{n,}`：`至少n个`的量词（也是`n到多个`的量词），如`/a{1,}/`，就和`/a+/`的作用一样
 
------
 
> - `^`：`以某某开头`的量词，如`/^abc/`, 表示以`abc`开头
> - （`注意`这里`/[^a]/`和`/^a/`的区别：中括号`里面的^a`表示`非a`，但中括号`外面的^`则是表示`以a开头`）
 
 
 
```javascript
let str = 'amabaaaaacccaaaddaa'
let reg = /^aba/
console.log(reg.test(str)) // false
```
 
 
 
------
 
> - `$`：`以某某结尾`的量词，如`/abc$/`, 表示以`abc`结尾
 
 
 
```javascript
let str = 'amabaaaaacccaaaddaa'
let reg = /dda$/
console.log(reg.test(str)) // false
```
 
 
 
------
 
> - `(?=)`：`修饰匹配`的量词，如`/\w\w(?=c)/`，表示匹配`后面紧跟c`的两位值
 
 
 
```javascript
let str = 'abcmdcttksfec'
let reg = /\w\w(?=c)/g
console.log(str.match(reg)) // ["ab", "md", "fe"]
```
 
 
 
------
 
> - `(?<=)`：`修饰匹配`的量词，如`/(?<=c)\w\w/`，表示匹配`前面紧跟c`的两位值
 
 
 
```javascript
let str = 'abcmdcttksfec'
let reg = /(?<=c)\w\w/g
console.log(str.match(reg)) // ["md", "tt"]
```
 
 
 
------
 
> - `(?!)`：`修饰匹配`的量词，如`/\w\w(?!c)/`，表示匹配后面`不紧跟c`的两位值
 
 
 
```javascript
let str = 'abcmdcttksfec'
let reg = /\w\w(?!c)/g
console.log(str.match(reg)) // ["bc", "dc", "tt", "ks", "ec"]
```
 
 
 
------
 
### `贪婪`与`非贪婪`模式
 
> 1、贪婪模式：`正则的默认模式`：一般趋向于最大长度匹配。
>
> 2、非贪婪模式：反之，取最小长度匹配
>
> 3、如何区分：在`量词（* + ? {m,n}）后面`加上`?`号，就是`非贪婪模式`
 
 
 
```javascript
const string = 'aabcaaabcccbabcabccab'
const regexp = /ab.*?cc/g
const regexp2 = /ab.*cc/g
console.log(string.match(regexp)) // [ 'abcaaabcc', 'abcabcc' ]
console.log(string.match(regexp2)) // [ 'abcaaabcccbabcabcc' ]
```
 
 
 
------
 
### 正则中的`复制`：使用`\1`或`\2`或`\3...`配合`()`来实现
 
> `\1`会复制正则里，`第一`个`()`里面的值
>
> `\2`会复制正则里，`第二`个`()`里面的值
>
> `\3`会复制正则里，`第三`个`()`里面的值
>
>...等等,以此类推
 
 
 
```javascript
// 如要取出字符串"abcdababcdcdcdjjaaaa"中`XOXO`这种类型的值
const string = "abcdababcdcdcdjjaaaa"
const regexp = /(\w)(\w)\1\2/g
 
console.log(string.match(regexp)) // [ 'abab', 'cdcd', 'aaaa' ]
```
 
 
 
------
 
### 可以使用正则的方法有哪些
 
> ```javascript
> let string = 'hello world!'
> let regexp = /llo/g
> ```
>
>
>
> - `regexp.test(string)`：返回布尔值，测试字符串`string`中是否有满足正则`regexp`的条件的字符串；
> - `regexp.exec(string)`：匹配正则里的值，并返回匹配时，所匹配的这个值的索引位置，也就是说`exec`可以`指出`正则在字符串的哪个`位置`匹配到了值。
 
> ```javascript
> console.log(regexp.exec(string)) // ["llo", index: 2, input: "hello world!", groups: undefined],
> ```
>
>
>
> - `string.match(regexp)`：返回匹配出的字符串`数组`；
> - `string.search(regexp)`：返回匹配到的字符串`位置（索引）`，没找到则返回`-1`；
> - `string.split(regexp)`：以匹配的正则的值为分割符，来将字符串`分割成数组`
> - `string.replace(regexp, 'another string')`：以正则来查找字符串，并将找到的正则值，替换为指定的字符串`another string`，最后返回新的修改后的字符串（注意replace这个方法是返回一个新字符串，原字符串不会被修改）
>
>
>
> ```javascript
> // string.replace()使用正则后，有两个特殊的地方
> // 1. #### 可以全局匹配
> console.log(string.replace('l','m')) // 'hemlo world!',可以看到，只会将第一个l替换成m
> regexp = /l/g
> console.log(string.replace(regexp,'m')) // 'hemmo wormd!',可以看到，会将所有l都替换成了m,当然正则必须添加g修饰符
> // 2. #### 可以在第二个参数里获取到正则()里的匹配到的正则值，就和上面讲到正则里的复制里的\1或\2一样
> string = 'aabbwwyymmnn' // 要求将所有的XXOO，替换成OOXX
> regexp = /(\w)\1(\w)\2/g
> console.log(string.replace(regexp,'$2$2$1$1')) // bbaayywwnnmm
> // 或
> console.log(string.replace(regexp,($,$1,$2)=> $2+$2+$1+$1)) // bbaayywwnnmm， 这种第二个参数是个回调函数的方式，更有实用价值一些， 回调函数里第一个形参$是`每次`正则匹配到的值，而第二个参数$1是正则里第一个子表达式(也就是正则里第一个小括号里)匹配到的值，第三个参数则是正则里第二个子表达式的匹配到的值。
> ```
 
 
 
## 正则的使用实例
 
 
 
> - 从字符串里：`首尾限定`来`选出需要的字符串`
 
 
 
```javascript
const mm = 'sfefaefhttps:www.chongly.com/sef/ff08fesfaef.jpg,asfeasi'
// 选出字符串里的图片
const reg = /http.*?\.jpg/i
const result = mm.match(reg)[0] // 打印出 https:www.chongly.com/sef/ff08fesfaef.jpg
```
 
 
 
> - 将字符串里的中划线名字，改成小驼峰规则的名字，比如`font-size`替换成`fontSize`
 
 
 
```javascript
const string = 'font-size;margin-top'
const regexp = /-(\w)/g // 注意这里需要使用子表达式，便于在replace的第二个参数里获取匹配到的值
console.log(string.replace(regexp, ($,$1) => $1.toUpperCase())) // 打印出 fontSize;marginTop
```
 
 
 
> - 将字符串里小驼峰规则的名字，改成中划线名字，比如`fontSize`替换成`font-size`
 
 
 
```javascript
const string = 'fontSize;marginTop'
const regexp = /[A-Z]/g
console.log(string.replace(regexp, $ => '-' + $.toLowerCase())) // 打印出 font-size;margin-top
```
 
 
 
> 1. 将`数字`进行`科学计数法`, 如`65236544115`转成`65,236,544,115`
 
 
 
```javascript
// 方法一：复杂易懂篇
const num = '165236544115'
let str_reverse = num.split('').reverse().join('') // 将字符串颠倒
const regexp = /(\d{3})(?!\b)/g // (?!\b)是防止最后一位后面也加上了,
const num_out = str_reverse.replace(regexp,'$1,')
console.log(num_out.split('').reverse().join('')) // 将颠倒的字符串，再颠倒回来
// 方法二：高端简洁篇
const num2 = '165236544115'
const regexp2 = /(?=(\B)(\d{3})+$)/g
console.log(num2.replace(regexp2, ','))
```