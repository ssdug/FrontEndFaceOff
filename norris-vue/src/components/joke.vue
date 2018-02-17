<template>
  <div>
    <div class="joke container">
      <div class="row">
        <div class="col-md-12">
          <h2>{{ msg }}</h2>
        </div>
      </div>
      <div class="row">
        <div class="offset-md-10 col-md-2">
          <!-- {{ randomCategory }}  -->{{selectedCategories}}
        </div>
      </div>
    </div>
    <div class="switchContainer">
      <toggle-button id="jokeSwitch"
          v-model="randomJokeEnabled"
          :width="250" :height="40"
          :color="{checked: 'green', unchecked: 'gray'}"
          :labels="{checked: 'NORRIS JOKES ON!!!', unchecked: 'I can not take anymore'}"
          />
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Joke',

  props: { // passed into component from parent using attributes
    selectedCategories: {
      type: Array,
      default: () => ([])
    },
    testing: true // if true it will use mock service to enable offline development
  },

  data () {
    return {
      msg: 'Pick a Category below',
      randomJokeEnabled: true, // bound to the button
      randomCategory: '' // holds the current category to pass to the service
    }
  },

  watch: { // watching for change so when toggled and on it will get the next joke
    randomJokeEnabled: {
      handler: function (val, oldVal) {
        if (val) {
          this.getJoke()
        }
      }
    }
  },

  methods: {
    jokeOn () { // method will determine if call to api should be made
      let vm = this
      if (vm.randomJokeEnabled) { // toggle must be on, maybe check for at least one category selected
        return true
      }
      return false
    },
    getJoke () {
      let vm = this
      if (vm.testing) {
        vm.getMockJoke()
      } else {
        vm.getAxiosJoke()
      }
    },
    getMockJoke () {
      let vm = this
      console.log('getMockJoke')
      let jokes = [
        'When Chuck Norris was born he round house kicked the Doctor in the face Slow mo\u0027 3 times for slapping his ass.',
        'Chuck Norris was once bitten by a rattlesnake in the desert, and after 3 days of pain and agony, the snake died.',
        'Chuck Norris likes his coffee half and half: half coffee grounds, half wood-grain alcohol.',
        'In the beginning there was nothing...then Chuck Norris Roundhouse kicked that nothing in the face and said \u0022Get a job\u0022. That is the story of the universe.'
      ]
      if (jokes.length > 0) { // does not care about cateory will just get a joke for display purposes
        var randomNumber = Math.floor(Math.random() * jokes.length)
        vm.msg = jokes[randomNumber]
      } else {
        vm.msg = 'No Joke'
      }
    },
    getAxiosJoke () {
      console.log('getAxiosJoke')
      let vm = this
      axios.get(`https://api.chucknorris.io/jokes/random?category=${vm.randomCategory}`)
        .then(function (response) {
          // console.log(response)
          vm.msg = response.data.value
        })
        .catch(function (error) {
          console.log(error)
        })
    }
  },

  created () {
    this.getJoke()

    // Requirement #4
    // As a classic javascript developer, I want to make a random joke appear every so many (5?) seconds on the website.
    setInterval(function () {
      if (this.jokeOn()) {
        this.getJoke()
      }
    }.bind(this), 10000)
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

  .joke {
    padding: 15px;
    background-color: #222;
  }

  .switchContainer {
    padding-top: 10px;
  }

  a {
    color: #42b983;
  }

  .vue-js-switch#jokeSwitch {
    font-size: 16px !important;
  }

  .vue-js-switch {
    margin: 2px;
  }
</style>
