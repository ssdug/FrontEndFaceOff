<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>
      <toggle-button id="jokeSwitch"
        v-model="randomJokeEnabled"
        :width="250" :height="40"
        :color="{checked: 'red', unchecked: 'green'}"
        :labels="{checked: 'MORE NORRIS JOKES!!!', unchecked: 'I can&quot;t take anymore'}"
         />
    </div>
    <h2>Essential Links</h2>
    <ul>
      <li>
        <a href="https://vuejs.org"
           target="_blank">
          Core Docs
        </a>
      </li>
      <li>
        <a href="https://forum.vuejs.org"
           target="_blank">
          Forum
        </a>
      </li>
      <li>
        <a href="https://chat.vuejs.org"
           target="_blank">
          Community Chat
        </a>
      </li>
      <li>
        <a href="https://twitter.com/vuejs"
           target="_blank">
          Twitter
        </a>
      </li>
      <br>
      <li>
        <a href="http://vuejs-templates.github.io/webpack/"
           target="_blank">
          Docs for This Template
        </a>
      </li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li>
        <a href="http://router.vuejs.org/"
           target="_blank">
          vue-router
        </a>
      </li>
      <li>
        <a href="http://vuex.vuejs.org/"
           target="_blank">
          vuex
        </a>
      </li>
      <li>
        <a href="http://vue-loader.vuejs.org/"
           target="_blank">
          vue-loader
        </a>
      </li>
      <li>
        <a href="https://github.com/vuejs/awesome-vue"
           target="_blank">
          awesome-vue
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
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
