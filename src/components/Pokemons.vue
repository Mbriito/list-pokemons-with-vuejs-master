<template>
    <div class="row">
        <h1>{{ msg }}</h1>
        <div class="col-xs-4 col-sm-2 col-md-2" v-for="pokemon in pokemons">
            <div class="thumbnail">
                <img :src="pokemon.sprites.front_default" alt="icon">
                <div class="caption">
                    <span v-for="type in pokemon.types" class="label label-default" style="margin-right: 2px;">{{ type.type.name }}</span>
                    <h3>{{ pokemon.name }}</h3>
                </div>
            </div>
        </div>
        <div class="col-xs-12">
            <nav>
                <ul class="pager">
                    <li class="previous" v-if="previous != null">
                        <a href="javascript:void(0);" v-on:click="searchPrevious()"><span aria-hidden="true">&larr;</span> Atras</a>
                    </li>
                    <li class="next" v-if="next != null">
                        <a href="javascript:void(0);" v-on:click="searchNext()">Siguiente <span aria-hidden="true">&rarr;</span></a>
                    </li>
                </ul>
            </nav>
        </div>
    </div>
</template>

<script>
  import Vue from 'vue'
  export default {
    name: 'Pokemons',
    data () {
      return {
        msg: 'List Pokemons!',
        pokemons: [],
        previous: null,
        next: null
      }
    },
    mounted: function () {
      this.getPokemons(Vue.config.env.API_REST + 'pokemon/?limit=100&offset=200')
    },
    methods: {
      getPokemons: function (url) {
        return window.fetch(url)
          .then(response => {
            return response.json()
          })
          .then(json => {
            this.next = json.next
            this.previous = json.previous
            return json.results
          })
          .then(results => {
            let data = []
            results.forEach(function (v, i) {
              window.fetch(v.url)
                .then(response => {
                  return response.json()
                })
                .then(json => {
                  data.push(json)
                })
                .catch(e => {
                  console.log('LOG_2 ' + e.message)
                })
            })
            this.pokemons = data
          })
          .catch(e => {
            console.log('LOG_1 ' + e.message)
          })
      },
      searchNext: function () {
        this.getPokemons(this.next)
      },
      searchPrevious: function () {
        this.getPokemons(this.previous)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
