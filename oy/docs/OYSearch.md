# OYSearch 搜索器组件

## Props

```ts
export interface IOYSearchProps extends IBaseProps {
  /**
   * 组件宽度
   */
  width?: number;
  /**
   * 输入最大长度
   */
  maxlength?: number;
  /**
   * 数据
   */
  dataSource: IOYSearchDataSource[];
  /**
   * 热门搜索
   */
  hotSearch?: string[];
  /**
   * 热门搜索颜色。如果是数组的化。会按顺序循环取色
  */
  hotSearchColor?: string[];
  /**
   * tab点击切换事件
   */
  onTabChange?: (item: IOYSearchDataSource, index: number) => void;
  /**
   * 点击搜索按钮
   */
  onSuffixClick?: (value: ISearchSuffix, index: number) => void;
  /**
   * 点击热门搜索
   */
  onHotSearchClick?: (value: string) => void;
  /**
   * input框focus事件
   */
  onFocus?: (event: InputEvent) => void;
  /**
   * input框blur事件
   */
  onBlur?: (event: Event) => void;
  /**
   * 点击搜索事件
   */
  onSearch?: (data: { dataSourceId: any; suffixId: any, value: string }) => void;
  /**
   * 点击最近搜索item事件
   */
  onDatalistClick?: (data: { value: string; dataSourceId: any; }) => void;
  /**
   * 自动补全点击事件
   */
  onAutoCompleteClick?: (data: { value: string; dataSourceId: any; }) => void;
}

export interface IOYSearchDataSource {
  /**
   * id
   */
  id: string;
  /**
   * tab名称
   */
  name: string;
  /**
   * placeholder
   */
  placeholder?: string;
  /**
   * 初始值
   */
  defaultValue?: string;
  /**
   * 后缀按钮配置
   */
  suffix?: ISearchSuffix[];
  /**
   * 下拉框配置
   * @description 当输入内容为空时显示的内容
   */
  datalist?: IOYSearchDatalist[];
  /**
   * 远程搜索自动补全
   */
  atuoComplete?: IOYSearchAtuoComplete;
}

export interface IOYSearchDatalist {
  /**
   * 分组标题
   */
  title: string;
  /**
   * 内容
   */
  options: string[]
}

export interface IOYSearchAtuoComplete {
  /**
   * 延迟触发时间间隔
   */
  delay?: number;
  /**
   *  远程搜索方法。
   * @param key 搜索值
   * @param response 响应回调函数
   */
  remote?: (key: string, response: (data: string[]) => void) => void;
}

export interface ISearchSuffix {
  /**
   * id
   */
  id: string;
  /**
   * 文本标签
   */
  label: string;
}

```

## Method

### getCurrentInputValue(): string

获取当前激活的输入框中的值

### setCurrentValue(value:string):void

设置当前激活的输入框中的值

## Example

```js


      // 搜索组件
      var searcInput = $("#oy-search").OYSearch({
        hotSearch: [],
        hotSearchColor: ['#999999', '#ed1b23'],
        dataSource: [
          {
            id: "package",
            name: '产品',
            defaultValue: '',
            placeholder: "牌号 / 品种 / 规格 / 仓库 / 产地",
            suffix: [{ id: 'packageShop', label: "搜本店" }, { id: 'packageArea', label: "搜全站" }],
            datalist: [{ title: '最近搜索', options: ['sss', 'bb'] }],
            atuoComplete: {
              delay: 200,
              remote: function (key, response) {
                setTimeout(function () {
                  response(['111', '222', '333'])
                }, 500)
              }
            }
          },
          {
            id: "shop",
            name: '店铺',
            defaultValue: '',
            placeholder: "店铺名称",
            suffix: [{ id: 'shopArea', label: "搜全站" }],
            datalist: [{ title: '店铺', options: ['店铺1', '店铺2'] }]
          }
        ],
        onTabChange: function (tab, index) {
          console.log('tabchange', tab, index)
        },
        onSuffixClick: function (val) {
          console.log(val);
        },
        onHotSearchClick: function (value) {
          this.setCurrentValue(value)
          console.log('onHotSearchClick', value)
        },
        onDatalistClick: function (value) {
          console.log('onDatalistClick', value)
        },
        onAutoCompleteClick: function (value) {
          console.log('onAutoCompleteClick', value)
        },
        onComponentDidMount() {
          console.log('onComponentDidMount')
        },
        onRender() {
          console.log('onRender')
        }
      });

```
