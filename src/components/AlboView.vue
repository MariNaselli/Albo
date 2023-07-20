<template>
    <div>
      <div v-if="apiResponse">
        <p>Fecha: {{ apiResponse.day }}/{{ apiResponse.month }}/{{ apiResponse.year }}</p>
        <p>Número: {{ apiResponse.num }}</p>
        <p>Título: {{ apiResponse.safe_title }}</p>
        <hr>
        <img :src="apiResponse.img" alt="Comic Image" width="300"  />
        <button @click="fetchComic(apiResponse.num - 1)">Anterior</button>
        <button @click="fetchComic(apiResponse.num + 1)">Siguiente</button>
        
      </div>
      <div v-else>
        Cargando...
      </div>
    </div>
  </template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      apiResponse: null,
    };
  },
  mounted() {
    this.fetchComic(100); // Obtener los datos de la caricatura 100 al cargar la página
  },

  methods: {
    fetchComic(comicNumber) {
      axios
        .get(`https://xkcd.vercel.app/?comic=${comicNumber}`)
        .then((response) => {
          this.apiResponse = response.data;
        })
        .catch((error) => {
          console.error("Error al obtener la caricatura:", error);
        });
    },
  },
};

</script>

<style></style>
