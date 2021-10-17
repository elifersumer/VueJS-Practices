<template>
    <div class="row">
        <div class="col-md-6 offset-md-3 border d-flex flex-row justify-content-between align-items-center pt-2 pb-2">
        <span>{{customer.firstName}} {{customer.lastName}}</span>
        <span>{{customer.customerNo}}</span>
        <button class="btn btn-danger" @click="$emit('deleteCustomer',customer.id)">Delete</button>
        </div>
      </div>
</template>

<script>
export default {
    props:["customer"],
    methods: {
    },
}
</script>

<style>

</style>