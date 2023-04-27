<template>
<v-container>
  <v-row>
    <v-col cols="8" md="4">
      <v-text-field
      outlined
      label="Buscar restaurante"
      dense
      prepend-icon="mdi-magnify"
      ></v-text-field>
    </v-col>
    <v-col cols="4" md="4">
      <v-btn @click="sortByName">Ordenar por Nombre</v-btn>
    </v-col>
    <v-col cols="4" md="4">
      <v-btn @click="sortByRaiting">Ordenar por Calificación</v-btn>
    </v-col>
  </v-row>




  <v-row>


    <v-col  :search="search" v-for="(item, index) in items" :key="index" cols="12" md="4" sm="4">
          <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="300"
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      src="https://cdn.foodandwineespanol.com/2019/01/regresar_comida.jpg"
    ></v-img>

    <v-card-title>{{ item.name }}</v-card-title>

    <v-card-text>
      <v-row
        align="center"
        class="mx-0"
      >
        <v-rating
          :value="item.rating"
          color="amber"
          dense
          half-increments
          readonly
          size="14"
        ></v-rating>

        <div class="grey--text ms-4">
          {{item.rating}}
        </div>
      </v-row>

      <div class="my-4 text-subtitle-1">
        $ • Restaurante
      </div>

      <div>Small plates, salads & sandwiches - an intimate setting with 12 indoor seats plus patio seating.</div>
    </v-card-text>

    <v-divider class="mx-4"></v-divider>




    <v-card-actions>
      <v-btn
        color="deep-purple lighten-2"
        text
        @click="reserve"
      >
        Ubicación
      </v-btn>
    </v-card-actions>


  </v-card>

    </v-col>
  </v-row>
</v-container>


</template>

<script>
export default {
  data() {
    return {
       items: [],
       coordinates: null,
       search: '',
    };
  },
   mounted() {
    this.getData()




  },
  methods: {

    /* OBTENEMOS EL ARREGLO DE LA PETICIÓN GET */
    getData(){
      this.$axios
        .get('https://recruiting-datasets.s3.us-east-2.amazonaws.com/data_melp.json' ,{
        })
        .then((response) =>{
          console.log(response)
          const obj = response.data

          const tamano = obj.length
          for (let i = 0; i < tamano; i++){
            const objeto = {
              name: obj[i].name,
              rating: obj[i].rating,
              lat: obj[i].address.location.lat,
              lng: obj[i].address.location.lng
            }
            this.items.push(objeto)
          }
           alert(response.data[0].address.location.lng)
        })
    },
     sortByName() {
      this.items.sort((a, b) => (a.name > b.name ? 1 : -1));
    },
    sortByRaiting() {
      this.items.sort((a, b) => a.rating - b.rating);
    },



  }
};
</script>

