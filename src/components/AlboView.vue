<template>
    <v-container fluid>
      <v-row justify="center">
        <v-col cols="12" sm="8" md="6">
          <v-card>
            <v-card-text>
              <div v-if="apiResponse" style="text-align: center;">
                <h2>{{ apiResponse.safe_title }}</h2>
                <p>Fecha: {{ apiResponse.day }}/{{ apiResponse.month }}/{{ apiResponse.year }}</p>
                <p>Número: {{ apiResponse.num }}</p>
                <hr>
                <div style="display: flex; align-items: center; justify-content: center;">
                  <button @click="fetchComic(apiResponse.num - 1)">&#8249;</button>
                  <img :src="apiResponse.img" alt="Comic Image" width="300" />
                  <button @click="fetchComic(apiResponse.num + 1)">&#8250;</button>
                </div>
              </div>
              <div v-else style="text-align: center;">
                <p>Cargando...</p>
              </div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
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
