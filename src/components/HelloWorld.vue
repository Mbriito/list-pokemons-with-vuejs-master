<template>
    <div class="hello">
        <img src="../assets/logo.png"/>
        <h1>{{ msg }}</h1>
        <a href="pokemons">Siguiente</a>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to the world Pokemon GO!'
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
  color: #fa2e13;
}
</style>
iuu