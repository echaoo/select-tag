<template>
  <div class="select-box-container">
    <select-box-left-panel @click-tab="changeTab" :data="data" @click-item="changeItem"></select-box-left-panel>
    <select-box-index></select-box-index>
    <select-box-right-panel :data="data.secondTabs[data.activeTab].items[data.secondTabs[data.activeTab].activeIndex]" @select-change="handleSelectChange"></select-box-right-panel>
  </div>
</template>

<script>
  import SelectBoxLeftPanel from './SelectBoxLeftPanel.vue';
  import SelectBoxRightPanel from './SelectBoxRightPanel.vue';
  import SelectBoxIndex from './SelectBoxIndex.vue';
  export default {
    props: {
      data: {
        type: Object,
        require: true
      }
    },
    methods: {
      changeTab(index) {
        this.data.activeTab = index;
      },
      changeItem({item, index}) {
        console.log('click item: ' + JSON.stringify(item));
        this.data.secondTabs[this.data.activeTab].activeIndex = index;
      },
      handleSelectChange(rs) {
        rs.thirdCate = this.data.secondTabs[this.data.activeTab].activeIndex;
        rs.secondCate = this.data.activeTab;
        console.log('change item: ' + JSON.stringify(rs));
        this.$emit('select-change', rs);
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
