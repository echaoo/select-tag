<template>
  <div class="right-panel-container">
    <h1 class="list-title">已选择 <span>0</span>/<span>10</span>个标签</h1>
    <div v-if="data.level == 2">
      <div class="first-list">
        <ul class="cas-panel">
          <li class="cas-item" v-for="(item, index) in data.selectList"
              :class="{'tab-active': index == data.activeIndex}" v-on:click="handleCateClick(item, index)"
          >
            {{item.name}}
          </li>
        </ul>
      </div>
      <div class="second-list">
        <ul class="cas-panel">
          <li class="cas-item" v-for="(item, index) in data.selectList[data.activeIndex].list">
            <input type="checkbox" :value="item.id" v-model="item.selected" :id="item.id"
                   v-on:click="handleItemClick(item, index)"><label class="label" :for="item.id">{{item.name}}</label>
          </li>
        </ul>
      </div>
    </div>
    <div v-if="data.level == 1">
      <ul class="cas-panel">
        <li class="cas-item" v-for="(item, index) in data.selectList">
          <input type="checkbox" :value="item.id" v-model="item.selected" :id="item.id" v-on:click="handle1LevelItemClick(item, index)"><label class="label" :for="item.id">{{item.name}}</label>
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
      handleCateClick(item, index) {
        console.log('click item:' + JSON.stringify(item));
        this.data.activeIndex = index;
      },
      handleItemClick(item, index) {
        let rs = {};
        rs.level = 5;
        rs.name = item.name;
        rs.id = item.id;
        rs.itemIndex = index;
        rs.fourthCate = this.data.activeIndex;
        console.log('change item: ' + JSON.stringify(rs));
        this.$emit('select-change', rs);
      },
      handle1LevelItemClick(item, index) {
        let rs = {};
        rs.level = 4;
        rs.name = item.name;
        rs.id = item.id;
        rs.itemIndex = index;
        console.log('change item: ' + JSON.stringify(rs));
        this.$emit('select-change', rs);
      }
    }
  }
</script>

<style>
  .right-panel-container {
    width: 380px;
    display: inline-block;
  }

  .list-title {
    font-size: 14px;
    border-bottom: 1px solid #d2d2d2;
    padding: 0 0 5px 10px;
  }

  .first-list {
    width: 190px;
    display: inline-block;
  }

  .first-list::-webkit-scrollbar {
    width: 0
  }

  .second-list {
    float: right;
    width: 190px;
    display: inline-block;
  }

  .second-list::-webkit-scrollbar {
    width: 0
  }
</style>
