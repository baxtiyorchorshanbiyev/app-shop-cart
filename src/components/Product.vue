<template>
  <el-container class="container">
  <el-row>
  <el-col v-for="(list, index) in lists" :key="index" :xl="5" :lg="5" :md="7" :sm="7" :xs="20" style="margin:10px 20px;">
    <el-card :body-style="{ padding: '0px' }" shadow="hover">
      <img src="https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8cGhvbmV8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60" class="image">
      <div class="product-info" style="padding: 14px;">
        <div class="product-avatar">
            <div class="product-type">
          <span>{{list.product_type}}</span>
        </div>
        <div class="product-time">
          <span>Kiritildi: {{list.author}} </span>
        </div>
        </div>
        <div class="product-about">
          <h4 class="product-name">{{list.product_name}}</h4>
          <p class="product-bio">{{list.product_title}}</p>
        </div>
        <div class="product-buy">
          <h4 class="price"><span>price: </span>{{list.product_price}}$</h4>
          <div>
            <el-button @click="addCart()" class="btn" icon="el-icon-s-goods" circle></el-button>
          </div>
        </div>
      </div>
    </el-card>
  </el-col>
</el-row>
  </el-container>
</template>
<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';
Vue.use(VueAxios,axios)
export default {
name:"Product",
data() {
  return{
    lists: undefined,
    id: null,
    }

},
mounted() {
this.getList()
},
methods: {
  getList(){
  Vue.axios.get(`https://616e5323a83a850017caa91c.mockapi.io/api/shop//users`)
  .then((res) =>{
    this.lists = res.data
  })
  },
    deleteCart(id) {
      Vue.axios.delete("https://616e5323a83a850017caa91c.mockapi.io/api/shop//users/"+id)
      .then(() =>{
        this.getList()
        
      })
    }
}
}
</script>

<style>
.container{
  width: 100%;
  display: block;
}
  .product-avatar{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .product-avatar span{
    font-size: 13px;
    color: #999;
  }
  .product-about{
    padding: 5px 0px;
    text-align: start;
  }
  .product-about p{
    font-size: 16px;
    color: #444;
    padding: 5px 0px;
  }
  .product-buy{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .product-buy .btn{
    background-color: #84CF6A;
    color: #fff;
    font-size: 18px;
  }
  .product-buy h4{
    color: #16C0B0;
    font-size: 18px;
  }
  .product-buy h4 span{
    font-size: 13px;
  }
  .button {
    padding: 0;
  }

  .image {
    width: 100%;
    display: block;
  }
</style>