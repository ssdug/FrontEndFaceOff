<template>
  <div class="hello">
    <Cat>
    </Cat><br />
    <njoke></njoke>
  </div>
</template>

<script>
import Categories from './Categories'
import joke from './joke'
export default {
  name: 'HelloWorld',
  components: {
    Cat: Categories,
    njoke: joke
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
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
