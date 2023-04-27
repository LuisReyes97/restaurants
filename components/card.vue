<template>
<v-container>
  <!-- botones de filtrados -->
  <v-row>
    <v-col cols="12" md="6" sm="6">
      <v-text-field
      outlined
      label="Buscar restaurante"
      dense
      prepend-icon="mdi-magnify"
      ></v-text-field>
    </v-col>
    <v-col cols="6" md="3" sm="4">
      <v-btn color="primary" @click="sortByName">Ordenar por Nombre</v-btn>
    </v-col>
    <v-col cols="6" md="3" sm="4">
      <v-btn color="success" @click="sortByRaiting">Ordenar por Calificación</v-btn>
    </v-col>
  </v-row>




  <v-row>


    <v-col  v-for="(item, index) in items" :key="index" cols="12" md="4" sm="4">
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
    >
    </v-img>

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
        $$ • Buffet libre
      </div>

      <div><strong>Opciones de servicios: </strong> Lorem ipsum dolor sit amet consectetur adipisicing elit. </div>

    </v-card-text>

    <v-list-item>
      <v-list-item-icon>
        <v-icon>mdi-phone</v-icon>
      </v-list-item-icon>
      <v-list-item-subtitle>{{item.phone}}</v-list-item-subtitle>
    </v-list-item>




    <v-divider class="mx-4"></v-divider>
    <v-card-actions class="white justify-center">
              <v-btn
                v-for="(social, i) in socials"
                :key="i"
                :color="social.color"
                class="white--text"
                fab
                icon
                small
                href="fb.com"
                target="_blank"
              >
                <v-icon >{{ social.icon }}</v-icon>
              </v-btn>
            </v-card-actions>




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
       socials: [
        {
          icon: 'mdi-facebook',
          color: 'indigo',
          url: 'www.facebook.com'
        },
        {
          icon: 'mdi-linkedin',
          color: 'cyan darken-1',
        },
        {
          icon: 'mdi-instagram',
          color: 'red lighten-3',
        },
      ],

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
              site: obj[i].contact.site,
              email: obj[i].contact.email,
              phone: obj[i].contact.phone,
              lat: obj[i].address.location.lat,
              lng: obj[i].address.location.lng

            }
            this.items.push(objeto)
          }
          /*  alert(response.data[0].address.location.lng) */
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

