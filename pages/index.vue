<template>
  <v-container>
    <v-row>
      <v-col v-for="(item, index) in items" :key="index" cols="12" md="4">
        <v-card>
          <v-card-title>{{ item.title }}</v-card-title>
          <v-card-text>{{ item.text }}</v-card-text>
          <v-card-actions>
            <v-btn color="primary">Acción 1</v-btn>
            <v-btn color="secondary">Acción 2</v-btn>
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
      items: [
        { title: 'Card 1', text: 'This is the first card' },
        { title: 'Card 2', text: 'This is the second card' },
        { title: 'Card 3', text: 'This is the third card' }
      ]
    }
  }

}
</script>
