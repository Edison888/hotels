<template>
<div>{{name}}</div>

</template>

<script>
const ERR_OK1 = 0
export default {
  name: 'details',
  data () {
    return {
      id: 0,
      hotels: [],
      name: ''
    }
  },
  created: function () {
    this.id = this.$route.query.id
    this.$http.get('./api/hotels').then((response) => {
      response = response.body
      if (response.errno === ERR_OK1) {
        this.hotels = response.data
        this.name = this.hotels[this.id].name
        console.log(this.hotels)
      }
    })
  }
}
</script>

<style>
#app {
}
</style>
