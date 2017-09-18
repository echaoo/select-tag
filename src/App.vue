<template>
  <div id="app">
    <select-tag :selectData="selectTagData" @change-tab="changeTab" @select-change="handleSelectChange"></select-tag>
  </div>
</template>

<script>
import SelectTag from './components/SelectTag.vue'
import selectData from './assets/MockData.json';

export default {
  name: 'app',
  data() {
    return {
      selectTagData: selectData,
      rs: []
    }
  },
  methods: {
    changeTab (index) {
      this.selectTagData.activeTab = index
    },
    handleSelectChange (rs) {
      if (rs.action === true) {
        if (this.selectTagData.currentSelect < this.selectTagData.totalSelect) {
          this.rs.push(rs)
          this.selectTagData.currentSelect++
        } else {
          if (rs.level === 5) {
            this.selectTagData.list[rs.firstCate].secondTabs[rs.secondCate].items[rs.thirdCate].selectList[rs.fourthCate].list[rs.itemIndex].selected = false
          } else if (rs.level === 4) {
            this.selectTagData.list[rs.firstCate].secondTabs[rs.secondCate].items[rs.thirdCate].selectList[rs.itemIndex].selected = false
          }
          alert('最多可选择' + this.selectTagData.totalSelect + '个标签！')
        }
      } else {
        this.rs.forEach((item, index) => {
          if (item.id === rs.id) {
            this.rs.splice(index, 1)
            this.selectTagData.currentSelect--
          }
        })
      }
      console.log(this.rs)
    }
  },
  components: {
    SelectTag
  }
}
</script>

<style>
#app {

}
</style>
