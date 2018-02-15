<template>
  <div>
    <coolVideo></coolVideo>
    <div class="toggleRow">
      <div class="rowItem">Local Mode - </div>
      <div class="rowItem">
        <div class="toggleButton">
          <div>Off&nbsp;</div>&nbsp;
          <toggle-button id="testingSwitch"
                         v-model="testing"
                         :width="40" :height="20"
                         :color="{checked: 'green', unchecked: 'gray'}" />
          &nbsp;<div>&nbsp;On</div>
        </div>
      </div>
    </div>

    <h2 class="title">{{msg}}</h2>
    <img class="image" src="../assets/Chuck-Norris-HD.jpg">
    <rjoke v-bind:testing="testing"></rjoke>
    <hr />
    <Cat v-bind:testing="testing">
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
      msg: 'Chuck Norris Vue(s)',
      testing: true
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
