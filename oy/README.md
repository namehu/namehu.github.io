# 欧冶 PC 插件文档

## 基于 jQuery、artTemplate 开发的欧冶插件。包含有搜索框、筛选器、排序插件等

## 说明

插件的编写形式一定程度上有React组件化思想的影响。所以在组件使用时。我们默认遵守一定的约定

### 插件列表

插件按照功能分类分为三大类。其中基础组件是提供了基础的UI组件。

主组件

- [OYSearch 搜索框](./docs/OYSearch.md)
- [OYFilter  筛选器](./docs/OYFilter.md)
- [OYOrderBar  排序组件](./docs/OYOrderBar.md)

工具组件

- [OYTool  工具方法](./docs/OYTool.md)

基础组件

- OYFilterBar
- OYIndustryComponet
- OYTab
- OYTag
- OYButton
- OYInput
- OYInputRange
- OYSelect
- OYCheckbox
- OYCheckbox2
- OYRadio
- OYRadioCheckbox
- OYDropdownInput
- OYDropdownInputRange
- OYCategoryTab

业务型组件

- OYFilterBarSaveList
- OYSpecification
- OYBalanceWeight
- OYFlag
- OYProductProp
- OYProductType

[组件生命周期](./docs/ComponentLifeCycle.md)  
[组件渲染流程](./docs/Componet.md)

### 参数(props)

插件的更新修改。都是通过传递参数值插件内部。插件会根据传入的参数自行渲染更新内容
参数选项我们称之为**props**。
修改更新插件统一使用**setProp**方法

例如

```js
// 实例化组件
var filter = $('oyfilter').OYFilter({ loading: true });

// 修改组件
filter.setProp({
  loading: false,
  value: {},
  data: []
})
```

### 方法(method)

修改渲染组件默认情况下都是基础**setProp**方法。当然组件也会提供一些方法来协助你做其他的事项。方法都是在组件实例上进行调用。组件具体提供的方法请参考具体的文档。

```js
// 获取筛选器的筛选参数
filter.getParams();

// 获取标签信息
filte.getTags();

```

当你对组件内部不是非常熟悉的情况下。请不要使用除上面以外的方式操作组件。不然很可能会出现意料之外的情形。

### 事件(event)

你需要针对组件发生的行为去做相应的处理。欧冶的组件都是基于事件回调函数机制来捕获组件中的各个行为。在回调函数中去处理你的业务逻辑。

**组件事件绑定支持多次绑定。多次绑定会按照绑定顺序依次执行。**

我提供了三种绑定事件回调函数的方式。下面我将逐个掩饰

#### 组件初始化时绑定

在组件实例化的时候。将事件放在props中传递给组件。

```js

var filter = $('filter').OYFilter({
  // 绑定筛选器参数变化时的事件
  onChange(value) {
    // do something when param change
  }
})
```
*组件实例化完成后。不能通过setProp方法传递事件函数！*

### on函数绑定

虽然不能通过setProp再次绑定事件函数。但是还可以通过on函数进行绑定。
绑定的形式有：

```js

// 通过on函数绑定回调
filter.on('onChange', function(value) {
   // do something when param change
})

// 可以绑定多个。
filter.on(['onChange','onSearch'], function(value) {
  // 'onChange','onSearch'都将触发这个回调函数
})

// on是可以忽略的
filter.on('change', function(value) {
   // onChange 和 change名称。效果是一样的。绑定的时候都将会被处理成onChange。所以可以放心使用
})
```

### addEvent

如果觉得每个都需要使用on函数绑定一遍太繁琐了那么声明式的写法方式你可能会喜欢

```js
// 声明式的写法，绑定onChange、onSearch事件
filter.addEvent({
  onChange: function() {

  },
  onSearch: function() {

  },
})
```

### 生命周期钩子事件回调

所有的插件都会有自己的生命周期。你可以根据这些事件钩子做一些额外的事情。

**onComponentDidMount**: 当组件首次挂载到浏览器dom上时。
当组件已经渲染完成并且首次渲染到浏览器界面里面时。会触发这个事件钩子

**onRender**: 组件渲染完毕之后
当组件每次渲染完毕之后。都会触发这个事件钩子

```js
filter.on(['onComponentDidMount', 'onRender'], () => {
  // 对组件生命周期绑定
})
```

