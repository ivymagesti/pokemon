<template>
  <div class="container">
        <div class="pokemonCard" v-for="pokemon in pokemons" :key="pokemon.name">
        <div class="card">
            <h1>{{ pokemon.name }}</h1>
            <img :src="pokemon.sprites.front_default" :alt="pokemon.name" />
            <ul class="type">
            <h2>Type:</h2>
            <li
                v-for="(type, index) in pokemon.types"
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
                <li v-for="(stat, index) in pokemon.stats" :key="index">
                <span
                    ><h3>{{ stat.stat.name }}: {{ stat.base_stat }}</h3></span
                >
                </li>
            </div>
            </ul>
        </div>
    </div>
    <button class="btn" @click="loadMore">Load More</button>
  </div>
</template>

<script>
import { pokeapi } from "@/api/pokeapi";

export default {
  data() {
    return {
      pokemons: [], // Inicialize a matriz de pokemons
      offset: 0, // Inicialize o offset para controle de paginação
      limit: 50, // Defina o limite de resultados por página
    };
  },
  methods: {
    async loadMore() {
      try {
        const response = await fetch(
          `${pokeapi}?offset=${this.offset}&limit=${this.limit}`
        );
        const data = await response.json();

        for (const result of data.results) {
          const pokemonResponse = await fetch(result.url);
          const pokemonData = await pokemonResponse.json();

          // Manipule os dados do Pokémon aqui, como alterar a capitalização do nome
          const capitalizedPokemonName =
            pokemonData.name.charAt(0).toUpperCase() +
            pokemonData.name.slice(1);
          pokemonData.name = capitalizedPokemonName;

          this.pokemons.push(pokemonData); // Adicione o Pokémon à matriz
        }

        this.offset += this.limit; // Atualize o offset para a próxima página
      } catch (error) {
        alert("Pokemon data could not be loaded");
      }
    },
  },
  mounted() {
    // Carregue os primeiros Pokémon quando o componente for montado
    this.loadMore();
  },
};
</script>

<style scoped>
.container {
  margin-top: 60px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center; /* Centraliza horizontalmente */
  align-items: center; /* Centraliza verticalmente */
}
.pokemonCard {
  margin: 10px;
  padding: 15px 10px;
  width: 500px; /* Largura padrão */
  height: 270px; /* Altura padrão */
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
  background: linear-gradient(
    90deg,
    rgb(251, 251, 250) 38%,
    rgb(255, 203, 5) 48%
  );
  flex-wrap: wrap;
}

.card {
  max-width: 50%;
  background: transparent;
  flex: 1;
  border: none;
  align-items: center;
}

img {
  max-width: 100%;
  display: block;
  margin-left: auto;
  margin-right: auto;
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
.data {
  max-width: 50%;
  flex: 1;
  color: rgb(0, 0, 0);
  font-family: "Press Start 2P", cursive;
  font-size: 1rem;
}

.list {
  padding-top: 15px;
  margin: 0 auto;
  text-align: justify;
  display: inline-block;
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

@media (max-width: 768px) {
  .pokemonCard {
    margin: 10px;
    padding: 15px 10px;
    width: 300px; /* Largura padrão */
    height: 270px; /* Altura padrão */
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
    background: rgb(255, 203, 5);
    flex-wrap: wrap;
  }
  h1 {
    font-size: 18px;
  }

  h2 h3 {
    font-size: 14px;
  }
  .data {
    display: none;
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
