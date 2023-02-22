<template>
  <div id="app">
    <div class="column">
      <div class="column is-half-one">
        <img class="imgassets" src="./assets/poke.png" />
        <input
          v-model="busca"
          class="input is-rounded"
          type="text"
          name=""
          id=""
          placeholder="Buscar pokemon pelo nome"
        />
        <button @click="buscar" class="button btn is-primary" id="buscaBtn">
          Buscar
        </button>
        <button class="button btn is-primary">
          <a href="/"> Voltar </a>
        </button>
        <div
          v-for="(poke, index) in filteredPokemons /*resultadoBusca*/"
          :key="poke.url"
        >
          <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log(res.data);
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar: function () {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name.toLowerCase() == this.busca.toLowerCase()
        );
      }
    },
  },
  computed: {
    /*
    resultadoBusca: function () {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    }, */
  },
};
</script>

<style scoped>
#app {
  color: #fff;
}
.imgassets {
  margin: 0 auto;
  display: block;
  width: 150;
}

.title {
  text-align: center;
}

input {
  margin: 0 auto;
  width: 300px;
  display: block;
  box-shadow: 0 0 16px 0 rgba(50, 214, 187, 0.486);
}

.btn {
  margin: 1rem auto;
  width: 300px;
  display: block;
  border-radius: 1.5rem;
}

a {
  text-decoration: none;
  color: white;
}
</style>
