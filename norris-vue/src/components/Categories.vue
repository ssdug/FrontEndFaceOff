<template>
  <div class="adsfasdf">
    <h2>Joke Categories</h2>
    <ul>
      <li v-for="cat in categories">
        {{ cat }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Categories',
  data () {
    return {
      categories: ['One', 'Two', 'Three'],
      msg: 'test this string'
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
