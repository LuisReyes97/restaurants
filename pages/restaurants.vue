<template>
<v-container>
<v-autocomplete
      v-model="name"
      outlined
      label="Busca tu restaurante"
      prepend-icon="mdi-magnify"
      dense
      required
    ></v-autocomplete>
  <card/>
</v-container>

</template>

<script>
import card from '~/components/card.vue'
export default {
  components: { card },

}
</script>
