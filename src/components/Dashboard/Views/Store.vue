<template>
    <div class="row">
      <div class="col-md-12">
        <div class="card">
        </div>
      </div>
      <input type="text" v-model= "product.name"> Name <br>
      <input type="text" v-model= "product.price"> Price <br>
        <button @click= "AddToApi"> add product</button> <br>
        <input type="text" v-model= "product.id"> product id <br>
          <button @click= "del"> del </button> <br>
        <table class="table table-striped table-borders">
        <thead>
        <tr>
        <th class="center"> ID </th>
        <th class="center"> Name </th>
        <th class="center"> Price </th>
        <th class="center"> Created at </th>
        <th class="center"> Updated at </th>
        <th class="center"> Seller Name </th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="prod in prods.data">
        <td class="test-left"> {{prod._id}}</td>
        <td class="test-left"> {{prod.name}}</td>
        <td class="test-left"> {{prod.price}}</td>
        <td class="test-left"> {{prod.createdAt}}</td>
        <td class="test-left"> {{prod.updatedAt}}</td>
        <td class="test-left"> Sama </td>
        </tr>
        </tbody>
        </table>
    </div>
</template>
<script>

import axios from 'axios'

export default {
  name: 'Store',
  data () {
    return {
      product: {
        id: '',
        name: '',
        price: '',
        createdat: '',
        updatedat: ''
      },
      prods: []
    }
  },
  mounted () {
    axios.get('http://localhost:3000/api/product/getProducts')
    .then(response => {
      console.log(response.data)
      this.prods = response.data
      console.log(prods)
    })
  },
  methods: {
    AddToApi () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        name: this.product.name,
        price: this.product.price
      })
    .then((response) => {
      console.log(response)
      console.log('Hi')
    })
    .catch((error) => {
      console.log(error)
    })
      window.location.reload()
    },
    del () {
      axios.delete('http://localhost:3000/api/product/deleteProduct' + '/' + this.product.id)
      .then((response) => {
        console.log(response)
        console.log('Hi')
      })
      window.location.reload()
    }
  }
}

</script>
<style>

</style>
