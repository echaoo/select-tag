# select-tag

> 一个多级选择框

demo: https://echaoo.github.io/demos/select_tag/

### 项目启动步骤

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

### 使用方法
> 输入数据格式请参照/src/assets/MockData.json

> 格式说明：本组件格式功能较为复杂，最多包括三层级联和两层tab切换，考虑到可能会有从外部删除的功能，因此输入数据结构设计的层级较深，具体说明如下(从最外层逐渐深入说明)：

##### 第一级：
- 对象list属性：Array，每一个元素代表最外层tab按钮内容， 如本例的"汽车兴趣"、"用户信息"按钮

- totalSelect属性: Number，定义共可以选择的标签数

- currentSelect属性： Number， 定义当前选择的表签数

- activeTab： Number， 定义当前层级active的按钮索引(默认为0，以下相同)

##### 第二级：
- tabName: String， 最外层按钮名称

- hasSecondTabs: Boolean，是否有第二层tab按钮（即本例的品牌，车型按钮， 如果没有第二层按钮，可以省略不写）

- secondTabs： Array， 每一个元素代表第二层按钮内容， 类似于第一级的list属性

- activeTab：  Number， 定义当前层级active的按钮索引

##### 第三级
- name： String， 第二级按钮名称

- items： Array， 第二级按钮包含的内容，为级联选择器第一级内容， 如本例的"最近一天访问车型"等

- activeIndex： Number， 定义当前层级active的按钮索引

##### 第四级
- name： String

- level: Number, 值为1和2， 定义后面的级联级数(例如，车型右侧面板有两级， 品牌有一级)

- selectList: Array， 每一个元素代表所包含的二级级联内容， 类似于第一级的list属性

- activeIndex: Number, 定义当前层级active的按钮索引

##### 第五级
- name： String

- id: String

- firstAlpha: String, 考虑到索引功能，需要知道每一项的首字母（首字母需要统一，大写或者小写）

- list: Array, 如果第四级level为2， 则会添加list属性， 为第三级的级联内容

- selected: Boolean, 如果第四级level为1， 则会添加selected属性，代表是否为选中值

- activeIndex: Number, 定义当前层级active的按钮索引 

##### 第六级
如果第四级level为2， 则会添加list属性， 为第三级级联内容

- name: String

- selected: Boolean, 判断是否为选中值

- id: String

#### Attributes
- selectData: Array, 选择框的所有内容

#### Events
- changeTab: 回调参数为当前点击按钮的index，用来改变最外层按钮切换效果 示例如下：
```vuejs
changeTab (index) {
      this.selectTagData.activeTab = index
    }
```
- handleSelectChange: 回调参数为已选择的checkBox的所有属性，用于选择内容发生变化时进行操作。

回调参数示例：
 ```javascript
[
  {
    action: true, // 表示此次点击为选中还是取消
    firstCate； 0，
    secondCate： 0，
    thirdCate： 0， 
    fourthCate： 0，
    itemIndex： 1， // 最后一级索引
    id: 2,
    name: '奥迪TT',
    level: 5 // 指所有层级，级联为2级时level为4， 级联为3级时level为5
  }
]
```
删除选择的内容示例：
```vuejs
handleSelectChange (rs) {
      this.selectTagData.list[rs.firstCate].secondTabs[rs.secondCate].items[rs.thirdCate].selectList[rs.fourthCate].list[rs.itemIndex].selected = false
    }
```





For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
