<template>
  <div class="select-box-container">
    <select-box-left-panel @click-tab="changeTab" :data="data" @click-item="changeItem"></select-box-left-panel>
    <select-box-index :alpha="indexArr" @index-click="changeJumpCount"></select-box-index>
    <select-box-right-panel :total-select="totalSelect" :current-select="currentSelect" :data="data.secondTabs[data.activeTab].items[data.secondTabs[data.activeTab].activeIndex]"
                            @select-change="handleSelectChange"
                            :scroll-distance="scrollDistance"></select-box-right-panel>
  </div>
</template>

<script>
  import SelectBoxLeftPanel from './SelectBoxLeftPanel.vue'
  import SelectBoxRightPanel from './SelectBoxRightPanel.vue'
  import SelectBoxIndex from './SelectBoxIndex.vue'

  export default {
    data() {
      return {
        scrollDistance: 0
      }
    },
    props: {
      data: {
        type: Object,
        require: true
      },
      totalSelect: {
        type: Number
      },
      currentSelect: {
        type: Number
      }
    },
    computed: {
      indexArr() {
        let tempArr = this.data.secondTabs[this.data.activeTab].items[this.data.secondTabs[this.data.activeTab].activeIndex].selectList
        let compare = function (prop) {
          return function (obj1, obj2) {
            if (obj1[prop] > obj2[prop]) {
              return 1
            } else if (obj1[prop] === obj2[prop]) {
              return 0
            } else {
              return -1
            }
          }
        }
        tempArr.sort(compare('firstAlpha'))
        let arr = this.setIndexData(tempArr, 30)
        return arr
      }
    },
    methods: {
      changeTab(index) {
        this.data.activeTab = index
      },
      changeItem({item, index}) {
//        console.log('click item: ' + JSON.stringify(item))
        this.data.secondTabs[this.data.activeTab].activeIndex = index
      },
      handleSelectChange(rs) {
        rs.thirdCate = this.data.secondTabs[this.data.activeTab].activeIndex
        rs.secondCate = this.data.activeTab
//        console.log('change item: ' + JSON.stringify(rs))
        this.$emit('select-change', rs)
      },
      setIndexData(data, height) {
        console.log(data)
        let indexCount = {}
        let temp = []
        let sum = 0
        for (let i = 0; i < data.length; i++) {
          if (i === 0) {
            indexCount[data[i].firstAlpha] = 0
            temp = []
            sum++
            temp.push(data[i])
            console.log(sum)
//          } else if (i !== 0 && i !== (data.length - 1)) {
          } else if (i !== 0) {
            if (data[i].firstAlpha !== data[i - 1].firstAlpha) {
              console.log(sum * height)
              indexCount[data[i].firstAlpha] = (sum * height)
              temp = []
            }
            sum++
            temp.push(data[i])
          }
//          else {
//            temp.push(data[i])
//            indexCount[data[i].firstAlpha] = (sum * height)
//          }
        }
//        console.log(indexCount)
        return indexCount
      },
      changeJumpCount(height) {
        this.scrollDistance = height
      }
    },
    components: {
      SelectBoxLeftPanel,
      SelectBoxIndex,
      SelectBoxRightPanel
    }
  }
</script>

<style>
  .select-box-container {
    background-color: #efefef;
    border: 1px solid #3eb368;
    margin: 0 20px 0 20px;
    height: 310px;
    width: 760px;
  }
</style>
