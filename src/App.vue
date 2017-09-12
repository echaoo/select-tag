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
    changeTab(index) {
      this.selectTagData.activeTab = index;
    },
    handleSelectChange(rs) {
      this.rs.push(rs);
      console.log(this.rs);
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
