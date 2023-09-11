<template>
  <section>
    <div class="search">
      <label for="pokemonInput">
        <input
          type="text"
          id="pokemonInput"
          placeholder="Name or ID"
          v-model="pokemonID"
        />
        <button class="btn" @click.prevent="searchPokemon">Search</button>
      </label>
    </div>

    <div class="show" v-if="Object.entries(pokemonData).length > 0">
      <div class="pokemonCard">
        <div class="card">
            <h1 class="pokemonName">{{ pokemonData.name }}</h1>
            <img
              :src="pokemonData.sprites.front_default"
              :alt="pokemonData.name"
            />
          <ul class="type">
            <h2>Type:</h2>
            <li
              v-for="(type, index) in pokemonData.types"
              :key="index"
              :class="type.type.name"
            >
              <span
                ><h3>{{ type.type.name }}</h3></span
              >
            </li>
          </ul>
        </div>
        <div class="data">
          <ul class="stats">
            <h1>Stats:</h1>
            <div class="list">
              <li v-for="(stat, index) in pokemonData.stats" :key="index">
                <span
                  ><h3>{{ stat.stat.name }}: {{ stat.base_stat }}</h3></span
                >
              </li>
            </div>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { pokeapi } from "@/api/pokeapi";

export default {
  name: "PokemonSearch",

  data() {
    return {
      pokemonData: {},
      pokemonID: "",
    };
  },

  methods: {
    async searchPokemon() {
      try {
        const pokemonToFind = await fetch(`${pokeapi}/${this.pokemonID}`);
        const pokemon = await pokemonToFind.json();
        this.pokemonData = pokemon;
        this.pokemonData.name =
          pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
        console.log(pokemon);
        return pokemon;
      } catch (error) {
        alert("Pokemon was not found");
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap");
.search {
  width: 100%;
  max-width: none;
  display: flex;
  align-items: center;
  justify-content: center;
  padding-right: 2rem;
  background: rgb(250, 247, 247);
  border-radius: 1rem;
  min-height: 7rem;
  height: auto;
  border-right: none;
  margin: 15px;
}
.btn {
  padding: 5px 10px;
  margin-left: 5px;
  background-color: #3763AD;
  border-radius: 4px;
  color: white;
  text-align: center;
  font-size: 1rem;
  box-shadow: 0 4px 8px rgba(30, 60, 90, 0.2);
  transition: all 0.3s;
  border: none;
  font-family: Arial, Helvetica, sans-serif;
  cursor: pointer;
}

.btn:hover {
  background: #154eb1;
  color: white;
  transform: scale(1.1);
}

.pokemonCard {
  margin: 0 auto;
  padding: 15px 10px;
  border-radius: 4px;
  color: black;
  text-align: center;
  font-size: 1rem;
  box-shadow: 0px 0px 24px 5px rgba(171, 171, 171, 1);
  border: none;
  font-family: "Press Start 2P", cursive;
  font-size: 0.5rem;
  display: flex;
  justify-content: space-between;
  max-width: 70%;
  background: linear-gradient(
    90deg,
    rgb(251, 251, 250) 41%,
    rgba(244, 21, 21, 1) 65%
  );
}

h1 {
  font-size: 22px;
}

h2 {
  font-size: 18px;
}
h3 {
  font-size: 14px;
}
.card {
  max-width: 50%;
  background: transparent;
  flex: 1;
  border: none;
  align-items: center;
}

.data {
  max-width: 50%;
  flex: 1;
  color: rgb(241, 235, 235);
  font-family: "Press Start 2P", cursive;
  font-size: 1rem;
}

.list {
  padding-top: 15px;
  margin: 0 auto;
  text-align: justify;
  display: inline-block;
}

img {
  max-width: 100%;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

@media (max-width: 768px) {
  .pokemonCard {
    margin: 10px;
    padding: 15px 10px;
    max-width: 100%; /* Largura padrão */
    height: 250px; /* Altura padrão */
    border-radius: 4px;
    color: black;
    text-align: center;
    font-size: 1rem;
    box-shadow: 0px 0px 24px 5px rgba(171, 171, 171, 1);
    border: none;
    font-family: "Press Start 2P", cursive;
    font-size: 0.5rem;
    display: flex;
    justify-content: space-between;
    background: rgba(244, 21, 21, 1);
    flex-wrap: wrap;
  }
  h1 {
    font-size: 18px;
  }

  h2 h3 {
    font-size: 14px;
  }
 
  .card {
  max-width: 100%;
  background: transparent;
  flex: 1;
  border: none;
  align-items: center;
}
}
</style>
