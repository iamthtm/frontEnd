<template lang="html">
  <div>

    name <input type="text" v-model="name">
    phone <input type="text" v-model="phone">
    <button @click="add(name, phone)">ส่ง</button>


    <hr> <br>
    <div v-for="show in list">
      {{show.name}} <br>
      {{show.phone}} <hr> <br>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list: [],
      name: '',
      phone: ''
    }
  },
  computed: {},
  methods: {
    getData: function () {
      let vm = this
      this.$http.get('http://localhost:3000/data').then(function (res) {
        vm.list = res.data
      })
    },
    add: function (name, phone) {
      var data = {
        name: name,
        phone: phone
      }
      this.$http.post('http://localhost:3000/data', data).then(function (res) {
        console.log(res)
      })
      // this.getData()
    }
  },
  components: {},
  mounted: function () {
    this.getData()
    var vm = this
    setInterval(function () {
      vm.getData()
    }, 2000)
  }
}
</script>

<style lang="css">
</style>
