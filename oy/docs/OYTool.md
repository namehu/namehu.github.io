# OYTool 工具函数

## 插件提供了一些方便的工具函数

### arrayFilter\<T = any\>(data: T[], fn: (el: T, index: number, data: T[]) => boolean): T[]

es6数组的[filter](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)方法。创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

```js
  var a = [1,2,3,4,-1,5,6,-4,7,8,9]

  $.OYTool.arrayFilter(a, function(item, index, data) { return item > 0 })

```

### objectOmit\<T extends { [i: string]: any } = {}\>(data: T, keys: (keyof T)[]): any

删除对象中指定的key数据

```js
  var data = {
    a: 1,
    b: true,
    c: function() {},
    d: '哈哈'
  };

  data = $.OYTool.objectOmit(data, ['c', 'b']);

  console.log(data);
  // {a: 1, d: '哈哈'}

```

### objectPick\<T extends { [i: string]: any } = {}\>(data: T, keys: (keyof T)[]): any

从对象中截取指定的key数据

`data` 数据
`keys` 需要选中的key

```js
  var data = {
    a: 1,
    b: true,
    c: function() {},
    d: '哈哈'
  };

  data = $.OYTool.objectPick(data, ['a', 'b']);

  console.log(data);
  // {a: 1, b: true}

```

### styles(data: { [i: string]: string }): string

将对象类型的style转换为字符串类型的样式文本

```js
  const sObj = $.OYTool.styles({
    width: 286,
    lineHeight: 36,
    height: 46,
    color: '#fff',
    zIndex: 20,
  })

  console.log(sObj);
  // 'width:"286px";line-height:"36px";height:"46px";color:"#fff";z-index:20'
```

### jointUrl(url: string, query: { [i: string]: any } = {}) :string

合并拼接url

```js

  var url = $.OYTool.jointUrl('http://localhost:8080/search-ng/queryResource/index', {
    mode:'package',
    newResource: 1,
    productType: 'BB10',
    heightSpec: '1,2',
  })

  console.log(url)
  // http://localhost:8080/search-ng/queryResource/index?mode=package&newResource=1&productType=BB10&heightSpec=1%2C2
```

### paseQuery(search = '') : {[i:string]:any}

解析url中的query参数

```js

  var query = $.OYTool.paseQuery('?mode=package&newResource=1&productType=BB10&heightSpec=1%2C2')

  console.log(query)
  // {   mode:'package',newResource: 1,productType: 'BB10',heightSpec: '1,2',}
```

### queryByKey(key:string): string | null

根据key查询url中的查询参数

```js
 var data = $.OYTool.queryByKey('newResource')
```

### formSubmit(url = '', data: { [i: string]: any }, method = 'get'): void

通过HTML表单提交

`url` 地址
`data` 表单数据
`method` 提交方法。默认为 get 方法 

```js
  $.OYTool.formSubmit(context.PATH + urlMap.search, formData)
```

### mergeQueryParam(param: { [i: string]: any }, map = getStringVavlueFilterParamMap()):void

将url中的query查询参数拼接成filter筛选器中的参数  

`param` url query参数
`map` 不需要传递

```js
$.OYTool.mergeQueryParam($.OYTool.paseQuery());
```

### getDefaultSortData(): any

获取默认的排序数据

```js
$.OYTool.getDefaultSortData();
```

### convertFastQueryParams(jsonParam: { [i: string]: any }) :any

将pc端旧的快查参数转换成为新的参数  

`jsonParam` 保存的快捷参数
