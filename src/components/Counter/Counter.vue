<template>
  <div class="number-container d-flex justify-content-center align-items-center">
    <!-- 减 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="subtract">-</button>
    <!-- 购买的数量 -->
    <span class="number-box">{{count}}</span>
    <!-- 加 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="add">+</button>
  </div>
</template>

<script>
  export default {
    data(){
      return {

      }
    },
    props:{
      count:{
        default:'',
        type:Number
      }
    },
    methods:{
      add(){
        this.$emit('addGoodsNum',this.count+1)
      },
      subtract(){
        if(this.count-1 <= 0) return 
        this.$emit('addGoodsNum',this.count-1)
      }
    }
  }
</script>

<style lang="less" scoped>
.number-box {
  min-width: 30px;
  text-align: center;
  margin: 0 5px;
  font-size: 12px;
}

.btn-sm {
  width: 30px;
}
</style>
