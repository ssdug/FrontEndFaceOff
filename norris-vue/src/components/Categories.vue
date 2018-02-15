<template>
  <div>
    <h2>Joke Categories</h2>
    <div class="container categories">
      <div v-for="(cat, i) in categories">
        <toggle-button class="categorySwitch"
              v-model="cat.Include"
              :key="i"
              :width="switchWidth" :height="switchHeight"
              :color="{checked: 'green', unchecked: 'gray'}"
              :labels="{checked: cat.Name, unchecked: cat.Name}"
              />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Category from '../model/category'

export default {
  name: 'Categories',

  props: {
    testing: true
  },

  data () {
    return {
      categories: {},
      msg: 'test this string',
      switchWidth: 200,
      switchHeight: 40
    }
  },

  watch: {
    categories: {  // watch the categories for changes; call getSelectedCategories to notify the parent  
      handler: function (val, oldVal) {
        this.getSelectedCategories()
      },
      deep: true // when watching an object properties use the handler and go deep
    }
  },

  methods: {
    getCategories () {
      let vm = this
      let data = []
      console.log(`testing: ${vm.testing}`)
      if (vm.testing) {
        data = vm.getMockCategories()
      } else {
        data = vm.getAxiosCategories()
      }
      vm.categories = data.map(function (obj) { return new Category(obj, false) })
    },
    getMockCategories () {
      console.log('getMockCategories')
      return ['dev', 'movie', 'food', 'celebrity', 'science', 'sport', 'political', 'religion', 'animal', 'history', 'music', 'travel', 'career', 'money', 'explicit', 'fashion']
    },
    getAxiosCategories () {
      console.log('getAxiosCategories')
      axios.get('https://api.chucknorris.io/jokes/categories')
        .then(function (response) {
          // console.log(response)
          return response.data
        })
        .catch(function (error) {
          console.log(error)
        })
    },
    getSelectedCategories () {
      let vm = this
      let selectedCategories = vm.categories.filter(function (el) {
        return el.Include === true
      })
      var categoryStrings = selectedCategories.map(a => a.Name)
      this.$emit('selectedCategories-changed', categoryStrings) // this will notify the parent that the object has changed
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

  .categories {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  a {
    color: #42b983;
  }

  .vue-js-switch {
    font-size: 20px;
  }
</style>
