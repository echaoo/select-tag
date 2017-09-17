<template>
  <div class="index">
    <ul>
      <li v-for="(item, index) in alphaList" @click="handleClick(item)">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      return {
//        alpha: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
      }
    },
    props: {
      indexKey: {
        type: Object,
        default() {
          return {}
        }
      },
      alpha: {
        type: Object,
        default () {
          return {}
        }
      }
    },
    computed: {
      alphaList () {
        return Object.keys(this.alpha)
      }
    },
    methods: {
      isDisable(index) {
        let temp = Object.keys(this.indexKey)
        for (let i = 0; i < temp.length; i++) {
          if (this.alpha[index] === temp[i]) {
            return false
          }
        }
        return true
      },
      handleClick(item) {
        this.$emit('index-click', this.alpha[item])
      }
    }
  }

</script>

<style>
  .disabled {
    color: #b4b4b4;
    cursor: not-allowed !important;
  }

  .disabled:hover {
    color: #b4b4b4;
    cursor: not-allowed !important;
    background-color: #d3d6d4 !important;
  }

  .index {
    width: 30px;
    height: 308px;
    background-color: #dbdedc;
    font-size: 12px;
    float: left;
    overflow-y: auto;
  }

  ::-webkit-scrollbar{width: 0}

  .index ul {
    margin: 0;
    padding: 5px 0 0 0;
    list-style: none;
  }

  .index ul li {
    padding: 1px 0 1px 8px;
  }

  .index ul li:hover {
    cursor: pointer;
    color: #fff;
    background-color: #3eb368;
  }
</style>
