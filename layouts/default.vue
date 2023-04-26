<template>
  <v-app dark>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
      color="orange darken-1"
    >
    <v-icon
      large
      color="orange lighten-5"
    >
      mdi-silverware-fork-knife
    </v-icon>
      <v-toolbar-title class="title">{{ title }}</v-toolbar-title>
      <v-spacer/>
      <v-card-subtitle>Inicio</v-card-subtitle>
      <v-card-subtitle>Restaurantes</v-card-subtitle>

    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer
      v-model="rightDrawer"
      :right="right"
      temporary
      fixed
    >
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light>
              mdi-repeat
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
<v-footer padless>
    <v-col
      class="text-center"
      cols="12"
    >
      {{ new Date().getFullYear() }} — <strong>Luis Reyes</strong>
    </v-col>
  </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        },

      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Melp'
    }
  }
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script&family=Montserrat:wght@500&display=swap');
  .title{
    font-family: 'Dancing Script', cursive;
    color: #F5F5F5;
  }

</style>


