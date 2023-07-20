<template>
  <v-app>
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
                
                <v-row align="center" justify="center">
                  <v-btn @click="fetchComic(apiResponse.num - 1)" class="arrow-btn left" icon>
                    <v-icon>mdi-chevron-left</v-icon>
                  </v-btn>
                  <img :src="apiResponse.img" alt="Comic Image" width="300" />
                  <v-btn @click="fetchComic(apiResponse.num + 1)" class="arrow-btn right" icon>
                    <v-icon>mdi-chevron-right</v-icon>
                  </v-btn>
                </v-row>
              </div>
              <div v-else style="text-align: center;">
                <p>Cargando...</p>
              </div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
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

<style>
/* Puedes eliminar los estilos personalizados, ya que usaremos las clases de tipografía de Vuetify */
.arrow-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  color: white;
  background-color: rgba(0, 0, 0, 0.5);
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
}

.left {
  left: 10px;
  z-index: 1;
}

.right {
  right: 10px;
  z-index: 1;
}
</style>



