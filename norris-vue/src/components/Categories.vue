<template>
  <div class="categories">
    <h2>Joke Categories</h2>
    <div class="container">
      <div class="row">
        <div class="col-lg" v-for="cat in categories">
          <toggle-button id="categorySwitch"
            v-model="category"
            :width="250" :height="40"
            :color="{checked: 'green', unchecked: 'gray'}"
            :labels="{checked: cat, unchecked: cat}"
            />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Categories',
  data () {
    return {
      categories: ['categories'],
      msg: 'test this string'
    }
  },
  methods: {
    getCategories () {
      let vm = this
      axios.get('https://api.chucknorris.io/jokes/categories')
        .then(function (response) {
          console.log(response)
          vm.categories = response.data
        })
        .catch(function (error) {
          console.log(error)
        })
    }
  },

  created () {
    this.getCategories()
  },

  mounted () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 5px 10px;
}
a {
  color: #42b983;
}

.vue-js-switch {
  font-size: 2em;
}
</style>
