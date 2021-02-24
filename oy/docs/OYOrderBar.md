# OYOrderBar 排序组件

## Props

```ts
interface IOYOrderBarProps extends IBaseProps {
  /**
   * 排序数据
   */
  data?: TOYOrderBarData[];
  /**
   * 排序规则
   */
  rules?: string[][];
  /**
   * publishPrice
   * @params 价格输入框
   */
  publishPrice?: string;
  /**
   * 价格搜索事件
   * @param value
   */
  onPublishPriceChange?(value: string): void;
  /**
   * 搜索框搜索事件
   * @param value
   */
  onSearch?(value: string): void;
  /**
   * 排序选项变化回调
   * @param data 变化后的排序数据
   */
  onChange?(data: ({ sortRule: string; sortType: any; } | null)[]): void;
}
```

## Method

### clearSort(emit:boolean):void

清空排序选项
参数emit: 是否触发onChange回调事件。默认不触发

## Example

```js
  
  const sortBar = $('#oy-sort-bar').OYOrderBar({
    publishPrice: '1-1000',
    rules: [['newResource', '*']],
  });

  sortBar.on('onChange', function(value) {
    console.log(value)
  })

```
