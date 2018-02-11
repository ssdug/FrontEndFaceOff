<template>
  <div>
    <coolVideo></coolVideo>
    <h2>{{msg}}</h2>
    <img src="../assets/Chuck-Norris-HD.jpg" style="width: 400px;">
    <rjoke></rjoke>
    <hr />
    <Cat>
    </Cat>
  </div>
</template>

<script>
import Categories from './Categories'
import RandomJoke from './Joke'
import Video from './Video'

export default {
  name: 'Home',
  components: {
    Cat: Categories,
    rjoke: RandomJoke,
    coolVideo: Video
  },

  data () {
    return {
      msg: 'Enlightenment! Compliments of Chuck Norris.'
    }
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
</style>
