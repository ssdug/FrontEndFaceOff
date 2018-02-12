<template>
  <div>
    <coolVideo></coolVideo>
    <h2 class="title">{{msg}}</h2>
    <img class="image" src="../assets/Chuck-Norris-HD.jpg" style="width: 400px;">
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

  .title {
    /*padding-bottom: 10px;*/
    margin: 0px 0 10px 0;
  }

  .image {
    width: 400px;
    margin: 10px 0 10px 0;
  }

  a {
    color: #42b983;
  }
</style>
