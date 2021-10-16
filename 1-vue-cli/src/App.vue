<template>
  <div class="container"> 
    <!-- <MainContainer/> -->
    <Product @AddToCart="cartItems.push($event)" :product="product" v-for="product in productList" :key="product.id"/>
    <!-- componentler arası veri taşıma için Vuex -->
    <h3>Sepet</h3>
    <div class="cart">
      <ul>
        <li v-for="item in cartItems" :key="item.id">{{item.title}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
//import MainContainer from "@/components/MainContainer"
import Product from "@/components/Product"
  export default{
      components:{
        //MainContainer,
        Product
      },
      data(){
        return {
          productList: [
                        {
                            id : 1,
                            title: "Laptop",
                            price: 10000,
                            amount: 45
                        },
                        {
                            id : 2,
                            title: "Phone",
                            price: 4000,
                            amount: 100
                        },
                        {
                            id:3,
                            title: "Earphone",
                            price: 200,
                            amount: 0
                        }
                    ],
                    cartItems : []
      }
      }
  }
</script>

<style>
.container{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>