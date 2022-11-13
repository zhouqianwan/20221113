<template>
  <div class="app-container">
   <Header></Header>
   <Goods v-for="item in list" 
   :key="item.id"
   :title="item.goods_name"
   :price="item.goods_price"
   :pic="item.goods_img"
   :state="item.goods_state"
   :id="item.id"
   
   @stateChange="getStateChange"
   >
    <Counter :count="item.goods_count" 
    @addGoodsNum="getAddNum(item,$event)"
    @subtractGoodsNum="getSubtractNum(item,$event)"
    ></Counter>
  </Goods>
   <Footer 
   :allState="allState"
   :goodsCount="allGoodsNum"
   :goodsPrice="allGoodsPrice"
   @sendAllState="getAllState"
   ></Footer>
  </div>
</template>

<script>
// 导入组件
import Header from '@/components/Header/Header.vue'
import Goods from '@/components/Goods/Goods.vue'
import Footer from '@/components/Footer/Footer.vue'
import Counter from '@/components/Counter/Counter.vue'
import axios from 'axios'
  export default {
    components: {
      Header,
      Goods,
      Footer,
      Counter
    },
    created(){
      this.initListData()
    },
    data(){
      return {
        list:[]
      }
    },
    methods:{
     async initListData(){
      const {data:res} = await  axios.get('https://www.escook.cn/api/cart')
        if(res.status==200){
          this.list = res.list
        }
      },
      getStateChange(val){
        // 调用some函数
        this.list.some((item)=>{
           if(item.id === val.id){
            item.goods_state = val.state
            return true
           }
        })
      },
      getAllState(val){
        this.list.forEach(item=>{
          item.goods_state = val
        })
      },
      getAddNum(i,val){
        this.list.some(item=>{
          if(item.id == i.id){
            item.goods_count = val
          }
        })
      },
      getSubtractNum(){
        this.list.some(item=>{
          if(item.id == i.id){
            item.goods_count = val
          }
        })
      }
      
    },
    computed:{
      allState(){
        // every方法，查看数组中所有的项是不是都满足这个条件
        return this.list.every(item=>{
          return item.goods_state 
        })
      },
      allGoodsNum(){
       return this.list.filter(item=>item.goods_state).reduce((all,item)=>{
          return all += item.goods_count
        },0)
      },
      allGoodsPrice(){
        return this.list.filter(item=>item.goods_state).reduce((total,item)=>{
          return total += item.goods_price*item.goods_count
        },0)
      }
    }
  }
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
