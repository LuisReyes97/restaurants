<template>


<div class="carousel-container">
  <v-carousel :show-arrows="false">
    <v-carousel-item
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
      expand
    ></v-carousel-item>
  </v-carousel>
  </div>
</template>

<script>
export default {
  data (){
    return{
items: [
          {
            src: 'https://get.wallhere.com/photo/food-wine-restaurant-steak-dessert-Sea-food-dinner-meal-cuisine-buffet-dish-christmas-dinner-supper-65559.jpg',
          },
          {
            src: 'https://wallpapercave.com/wp/wp3108291.jpg',
          },
          {
            src: 'https://cdn.vuetifyjs.com/images/carousel/bird.jpg',
          },
          {
            src: 'https://cdn.vuetifyjs.com/images/carousel/planet.jpg',
          },
        ],

    }
  },
  methods: {
    getdata(){
      this.$axios
        .get('https://recruiting-datasets.s3.us-east-2.amazonaws.com/data_melp.json',{
        })
        .then((res) => {
          console.log(res)
        })
    }
  },

  mounted() {
    this.getdata()
  }

}
</script>

<style>
.carousel-container {
  height: 100%;
}
</style>


