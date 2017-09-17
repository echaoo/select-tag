<template>
  <div class="left-panel">
    <p class="left-panel-title">标签类型</p>
    <div class="tab-button-group tag-btn-container" v-if="data.hasSecondTabs">
      <button class="switch-tag-btn" v-for="(item, index) in data.secondTabs" :class="{'tab-active': index == data.activeTab}" @click="handleTabClick(index)">{{item.name}}</button>
    </div>
    <div class="left-panel-select-box">
      <ul class="cas-panel">
        <li class="cas-item" v-for="(item, index) in data.secondTabs[data.activeTab].items" :class="{'tab-active': index == data.secondTabs[data.activeTab].activeIndex}" v-on:click="handleItemClick(item, index)">
          {{item.name}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

  export default {
    props: {
      data: {
        type: Object,
        require: true
      }
    },
    methods: {
      handleTabClick(index) {
        this.$emit('click-tab', index)
      },
      handleItemClick(item, index) {
        this.$emit('click-item', {item, index})
      }
    }
  }

</script>

<style>
  .left-panel {
    width: 350px;
    float: left;
  }

  .left-panel-title {
    margin: 5px 5px;
  }

  .switch-tag-btn {
    color: #4fbc7d;
    height: 24px;
    padding: 2px 10px;
    font-size: 12px;
    border: 1px solid #4fbc7d;
    background-color: #ffffff;
    margin-left: -1px;
    outline: none;
    cursor: pointer;
  }

  .tab-button-group {
    margin: 3px 15px;
  }

  .tab-active {
    background-color: #4fbc7d;
    color: #fff;
  }

  .left-panel-select-box {
    border-top: 1px solid #d2d2d2;
    width: 350px;
    height: 236px;
    overflow-y: auto;
    overflow-x: hidden;
    padding: 0;
    background: #efefef;
    margin: 15px 0 1px 0;
  }

  .cas-panel {
    margin: 0;
    padding: 0;
  }

  .cas-item {
    font-size: 14px;
    padding: 5px 5px 5px 15px;
    cursor: pointer;
    list-style: none;
  }

  .cas-item:hover {
    color: #fff;
    background-color: #4db262;
  }

</style>
