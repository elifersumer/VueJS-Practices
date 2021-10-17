<template>
  <div class="row">
    <div id="container">
    <div class="col-md-8 offset-md-2 text-center">
      <h3 class="mt-5">CUSTOMERS</h3>
      <hr>
      <div class="row">
        <div class="col-md-10 offset-md-1 border d-flex flex-row justify-content-between align-items-center pt-2 pb-2">
          <input type="text" placeholder="Enter first name" v-model="firstName">
          <input type="text" placeholder="Enter last name" v-model="lastName">
          <input type="number" placeholder="Enter customer number" v-model="customerNo">
          <button @click="addCustomer()" class="btn btn-primary">Add</button>
        </div>
      </div>
      <hr>
      <div class="customer-container">
        <Customer @deleteCustomer="deleteCustomer($event)" v-for="customer in customerList" :key="customer.id" :customer="customer"/>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import Customer from "@/components/Customer"
import axios from "axios"
export default {
  components:{
    Customer
  },
  data(){
    return{
      firstName : "",
      lastName : "",
      customerNo : null,
      id : null,
      customerList : []
    }
  },
  methods: {
    addCustomer(){
      axios.post("https://vuejs-practices-5020e-default-rtdb.firebaseio.com/customers.json",{firstName:this.firstName,lastName:this.lastName,customerNo:this.customerNo})
      .then(response=>{
        this.customerList.push({
          firstName: response.data.firstName,
          lastName: response.data.lastName,
          customerNo: response.data.customerNo,
          id: response.data.name
        })
      })
      .catch(e=>{
        console.log(e)
      })
    },
    deleteCustomer(id){
      axios.delete("https://vuejs-practices-5020e-default-rtdb.firebaseio.com/customers/" + id + ".json")
      .then(() => {
        let index = this.customerList.findIndex(i=>{
          return i.id==id
        })

        this.customerList.splice(index,1)
      })
      .catch(e=>{
        console.log(e)
      })
    }
  },
  created(){
      axios.get("https://vuejs-practices-5020e-default-rtdb.firebaseio.com/customers.json")
      .then(response=>{
        for(let key in response.data){
          let customer = {
            customerNo: response.data[key].customerNo,
            firstName: response.data[key].firstName,
            lastName: response.data[key].lastName,
            id: key
          }
          this.customerList.push(customer)
        }
      })
      .catch(e=>{
        console.log(e)
      })
    }
}
</script>

<style>

</style>
