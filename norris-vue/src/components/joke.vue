<template>
  <div>
    <h2>{{ msg }}</h2>
    <div>
      <toggle-button id="jokeSwitch"
        v-model="randomJokeEnabled"
        :width="250" :height="40"
        :color="{checked: 'red', unchecked: 'green'}"
        :labels="{checked: 'MORE NORRIS JOKES!!!', unchecked: 'I can not take anymore'}"
         />
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Joke',
  data () {
    return {
      msg: '',
      randomJokeEnabled: true
    }
  },
  methods: {
    getJoke () {
      let vm = this
      axios.get('https://api.chucknorris.io/jokes/random')
        .then(function (response) {
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
      if (this.randomJokeEnabled) {
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

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
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
