<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input type="text" placeholder="enter the name you search" v-model="val"/>
      <button @click="searchBtn">Search</button>
    </div>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  name: 'GaTop',
  data() {
    return {
      val: ''
    }
  },
  methods: {
    searchBtn() {
      this.$bus.$emit('traData', {searching:true})
      axios.get(`https://api.github.com/search/users?q=${this.val}`).then(
          response => {
            this.$bus.$emit('traData', {userInfo:response.data.items,searching:false})
            // this.$bus.$emit('traData', response.data.items)
          },
          error => {
            this.$bus.$emit('traData', {err:error})
          }
      )
    },
  }
}
</script>

<style>

</style>
