<template>  
  <div>
    <header class="encabezado">
      <h1><center>Pokemon Go</center></h1>
    </header>

    <main>
      <div class="pokemon" v-for="pokemon in pokemones" :key="pokemon.id">
        <img :src="pokemon.imagen" :alt="pokemon.nombre" />
        <h2 >{{ pokemon.nombre }}</h2>
        <span :style="{'background-color':pokemon.type_color }">{{ pokemon.type_name }}</span>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      pokemones: [] 
    };
  },
  mounted() {
    this.getPokemones(); 
  },
  methods: {
    getPokemones() {
      axios
        .get('https://cobuses.com.co/APIV2/model/pokemon.php?dato=getallpokemon')
        .then((response) => {
          this.pokemones = response.data.map(pokemon => ({
            ...pokemon,
          }));
        })
        .catch((error) => {
          console.log(error);
        });
    }
  }
};
</script>

<style>
main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 20px;
}

.pokemon {
  margin: 10px;
  padding: 10px;
  border-radius: 8px;
  width: 150px;
  text-align: center;
  background-color: #f3f3f3;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.pokemon img {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
}

.pokemon h2 {
  margin-top: 10px;
  font-size: 16px;
}
</style>
