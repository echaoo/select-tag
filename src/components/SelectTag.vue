<template>
  <div class="select-tag-container">
    <div class="title">
      <span>添加标签</span><span class="close" @click="handleClose(0)">X</span>
    </div>
    <div class="button-group">
      <button class="btn" v-for="(item, index) in selectData.list" :class="{'btn-active': index === selectData.activeTab}" @click="handleButtonClick(index)">{{item.tabName}}</button>
    </div>
    <select-box :data="selectData.list[selectData.activeTab]" @select-change="handleSelectChange"></select-box>
    <div class="footer">
      <button class="btn footer-btn" @click="handleClose(0)">取消</button>
      <button class="btn footer-btn" @click="handleClose(1)">确定</button>
    </div>
  </div>
</template>

<script>
  import SelectBox from './SelectBox.vue';

  export default {
    props: {
      selectData: {
        type: Object,
        require: true
      }
    },
    methods: {
      handleButtonClick(index) {
        this.$emit('change-tab', index)
      },
      handleClose(code) {
        this.$emit('close', code);
      },
      handleSelectChange(rs) {
        rs.firstCate = this.selectData.activeTab;
        console.log('change item: ' + JSON.stringify(rs));
        this.$emit('select-change', rs);
      }
    },
    components: {
      SelectBox
    }
  }

</script>

<style>

  .select-tag-container {
    position: absolute;
    top: 30px;
    left: 50%;
    margin-left: -400px;
    width: 800px;
    height: 488px;
    z-index: 101;
    /*box-shadow:2px 4px 10px 0 rgba(127,127,127,0.50);*/
    border: 2px solid #3eb368;
    border-radius: 3px;
    background-color: #ffffff;
  }

  .title {
    background-color: #3eb368;
    box-sizing: border-box;
    height: 40px;
    width: 100%;
    color: #fff;
    text-align: left;
    padding: 10px 0 0 20px;
    font-size: 14px;
  }

  .close {
    float: right;
    padding: 3px 10px;
    margin-right: 10px;
  }

  .button-group {
    margin: 20px 0 26px 20px;
  }

  .btn {
    color: #4fbc7d;
    width: 86px;
    height: 34px;
    font-size: 13px;
    border: 1px solid #4fbc7d;
    background-color: #ffffff;
    margin-left: -5px;
    outline: none;
    cursor: pointer;
  }

  .btn-active {
    background-color: #4fbc7d;
    color: #fff;
  }

  .footer {
    text-align: center;
  }

  .footer-btn {
    border-radius: 7px;
    margin: 15px;
  }

  .btn:hover {
    color: #fff;
    background-color: #3eb368;
  }

</style>
