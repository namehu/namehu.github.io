# OYFilter 筛选器

## Props

```ts
export interface IOYFilterProps extends IBaseProps {
  /**
   * 表格宽度
   */
  width?: number | string;
  /**
   * 标题宽度
   */
  titleWidth?: number;
  /**
   * 列表显示数量。超出的点击展开更多显示
   * 如果传入true则表示全部显示
   * @default 8
   */
  showItems?: number | boolean;
  /**
   * 选中的值
   */
  value: { [i: string]: any };
  /**
   * 数据
   */
  data: { [i: string]: IDataType };
  /**
   * 远程获取数据
   */
  // remoteData?: (params: any) => JQueryPromise<{ [i: string]: IDataType }>;
  /**
   * 是否在加载中
   */
  loading: boolean;

  /** industryComponet start */
  /**
   * 图片基础路径
   */
  industryComponetStaticPath?: string;
  /**
   * 爆炸图数据
   */
  industryComponet?: OYIndustryComponetData[];
  /** industryComponet stop */

  /** filterBar start */
  /**
   * 提供给tags的额外标签
   */
  tags?: IOYFilterBarTag[];
  /**
   * 快捷查询的数据
   */
  fastQueryList?: ISaveListData[];
  /**
   * 是否显示反馈icon
   */
  feedback?: boolean;
  /**
   * 是否显示反馈的tooltip
   */
  feedbackTooltip?: boolean | (() => boolean);
  /**
   * 点击反馈
   */
  onFeedbackClick?(): void;
  /**
   * 点击关闭反馈
   */
  onFeedbackClose?(): void;
  /**
   * 点击保存筛选条件
   */
  onSave?(): void;
  /**
   * 点击已保存筛选条件
   */
  onSaveListClick?(value: ISaveListData, index: number, list: ISaveListData[]): void;
  /**
   * 点击删除已保存筛选条件
   */
  onSaveListDelete?(value: ISaveListData, index: number, list: ISaveListData[]): void;
  /**
   * 点击移除标签
   * @param data
   * @param index
   */
  onTagRemove?(data: IOYFilterBarTag, index: number): void;
  /**
   * 点击重置标签
   */
  onTagReset?(): void;
  /** filterBar stop */
  /**
   * 在change之前回调函数。
   * 如果返回true。正常执行onChange
   * 如果返回false。则不触发onChange
   * @param value
   * @param keys
   * @description 针对特殊逻辑做处理
   */
  beforeChange?(value: string, keys: string[]): boolean;
  /**
   * 触发change事件
   * @param {string} value
   * @param {string[]} keys
   */
  onChange?(value: string, keys: string[]): void;
  /**
   * 触发搜索事件
   * @param params
   */
  onSearch?(params: any): void;
  /**
   * 爆炸图点击事件
   * @param name 名称
   * @param value 值
   */
  onIndustryComponetClick?(name: string, value: string): void;
  /**
   * 点击切换展开收起
   */
  onToogle?(): void;
  /**
   * 错误重载回调
   * 需要配合实例方法filter.showError方法使用
   * @description 在调用filter.showError()方法后。在显示的错误页面中点击重新加载才能触发该事件
   */
  onErrorReload?(): void;
  /**
   *  筛选器频道触发点击事件
   *
   * @param {{ value: string, name: string }} data 数据
   * @param {number} index 当前数据索引
   */
  onChannelClick?(data: { value: string, name: string }, index: number): void;
}
```

## Method

### setFastQueryList(data: ISaveListData[]):void

设置快捷保存数据。请确保filterBar存在。否则请使用fastQueryList props

### changeNumber(count?: number, totalWeight = 0):void

修改数量重量

### getTags():void

获取筛选栏中所有的tag

### getParams():void

获取筛选参数

### showError({ text, img }: { text: string, img: string }, cb?: () => {})

渲染错误页面。
参数
`text` 错误文本
`img` 错误图片

`cb` 点击重新加载后执行的回调函数。你也可以通过绑定`onErrorReload`事件进行处理


## Example

```js
  var filter = $('#oy-filter').OYFilter({
      loading: true,
      value: filterValue,
      data: filterData[0],
      fastQueryList: saveList[0],
      width: 960,
      titleWidth: 90,
      // showItems: true,
      beforeChange: function (value, keys) {
        if (keys[1] === 'newResource') {
          // 新资源点击校验登陆。如果没有登陆返回false。阻止触发change
          console.log('点击了新资源')
          return false;
        }
        return true
      },
      onChange: function (value) {
        console.log(value)
      },
      onSearch: function (value) {
        filter.setProp({ value: value })
        console.log('onSearch', value)
      }
    })
```
