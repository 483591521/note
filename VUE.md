### VUE el-data-picker 显示给定数组里面的日期

```vue
disabledDate (time) {
	const year = time.getFullYear()
	let month = time.getMonth() + 1
	let day = time.getDate()
	if (day < 10) day = '0' + day
    if (month < 10) month = '0' + month
	const ym = year + '-' + month + '-' + day
	return !dateArray.includes(ym)
}
```

### VUE 从对象中取key值和value值

- Object.keys(obj) 
- 参数(obj):** 要返回其枚举自身属性的对象。
- 返回值:** 一个表示给定对象的所有可枚举属性的字符串数组。

Object.keys 返回一个所有元素为字符串的数组，其元素来自于从给定的object上面可直接枚举的属性。这些属性的顺序与手动遍历该对象属性时的一致。

```vue
const obj={
	name:"yhh",
	sex:"女",
	work:"IT"
}
console.log(Object.keys(obj))
console.log(Object.values(obj))
```

