>&：两个都为1才为1，否则为0
>
>| ：有一个为1就为1，否则为0
>
>^ ： 相同为0不同为1，相同的数异或为0: n ^ n => 0，任何数于0异或为任何数 0 ^ n => n

1. 使用左移运算符<<迅速得出2的次方

```js
1 << 2 // 4 即2的2次方
1 << 10 // 1024 即2的10次方
// 但是要注意使用场景
a = 2e9 // 2000000000
a << 1 // 2000000000
```

2. 使用 & 判断奇偶性

```js
// 偶数 & 1 = 0
// 奇数 & 1 = 1

console.log(7 & 1);    // 1
console.log(8 & 1) ;   // 0
```

3. 使用!! 将数字转为布尔值

```js
// 所有非0的值都是true,包括负数，浮点数

console.log(!!7);       // true
console.log(!!0);       // false
console.log(!!-1);      // true
console.log(!!0.71);    // true
```

4. 使用 ~ ，>> ，<< ，>>> ，| 来取证

```js
// 相当于使用了Math.floor()
// >>> 不可对负数取整

console.log(~~11.71)     // 11
console.log(11.71 >> 0)  // 11
console.log(11.71 << 0)  // 11
console.log(11.71 | 0)   // 11
console.log(11.71 >>> 0) // 11
```

5. 使用 ^ 来完成值交换

```js

// --- before ---
let temp = a; a = b; b = temp; // 传统，但需要借助临时变量
b = [a, a = b][0] // 借助数组

// --- after ---
let a = 7
let b = 1
a ^= b
b ^= a
a ^= b
console.log(a)   // 1
console.log(b)   // 7

[a, b] = [b, a]; // ES6，解构赋值
```

6. 使用 ^ 判断符号是否相同

```js
(a ^ b) >= 0; // true表示相同，false表示不同

let x = -1
let y = 11
console.log(x ^ y) // -12
x = 2
console.log(x ^ y) // 9
```

7. 使用 ^ 来检查数字是否相等

```js

// --- before ---
if (a !== 1171) {...};

// --- after ---
if (a ^ 1171) {...};
               
let a = 1171
if (a ^ 1171) { // 没有输出因为 任何数异或它本身为0,而0为false
    console.log("equal.")
}
if (a ^ 7777) { // 除了0之外的数都是true
	console.log("Not equal")
}
```

8. n & (n - 1) 如果为0，说明n是2的整数幂

```js
let n = 24
console.log(n & (n-1))
n = 64
console.log(n & (n-1))
```

9. 使用 (A+0.5 | 0) 来代替Math.round() 如果是负数则-0.5

```js
let a = 24.7
console.log(Math.round(a)) // 25
console.log(a + 0.5 | 0) // 25

a = 24.1
console.log(Math.round(a)) // 24
console.log(a + 0.5 | 0) // 24

a = -24.1
console.log(Math.round(a)) // -24
console.log(a - 0.5 | 0) // -24
```

10. 使用toString(16) 取随机字符串

```js
// .substring()的第二个参数控制取多少位(最多可取13位)

Math.random().toString(16).substring(2, 15)
console.log(Math.random().toString(16).substring(2, 4)) // 9a
console.log(Math.random().toString(16).substring(2, 8)) // e8683a
console.log(Math.random().toString(16).substring(2, 15)) // fe23299a7d85c
console.log(Math.random().toString(16).substring(2, 30)) // de728c6853ecd
```

11. 使用split(0), 使用数字来作为split的分隔条件可以节省2字节

```javascript

// --- before ---
"alpha,bravo,charlie".split(",");

// --- after ---
"alpha0bravo0charlie".split(0);
```

12. 使用.link()创建连接，可以快速创建a标签

```javascript
let b = '<a href="www.baidu.com">baidu</a>'
console.log(b) // <a href="www.baidu.com">baidu</a>
let a = "baidu".link('www.baidu.com')
console.log(a) // <a href="www.baidu.com">baidu</a>
```

13. 创建随机数

```js
let b = 0 | Math.random() * 100
console.log(b)
```

