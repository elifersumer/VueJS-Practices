<template>
    <div class="product" >
        <strong>{{product.title}}</strong>
        <p>{{product.amount}}</p>
        <strong>Fiyatı: {{product.price}} TL</strong>
        <hr>
        <button @click="AddToCart(product)">Sepete Ekle</button>
    </div>
</template>

<script>
export default {
    props : ["product"],
    methods: {
     AddToCart(product){
         this.$emit("AddToCart", product)
     }   
    },
};
</script>

<style>
.product{
    color: black;
  border: 2px dashed #666;
  padding: 5px 10px;
  width: 300px;
  margin-right: 10px;
}

.product:hover{
  border: 2px solid #666;
}
</style>