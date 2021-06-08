<template>
  <v-app id="inspire">
    <v-container fluid>
        <v-row dense>
          <v-col  
            v-for="card in cards"
            :key="card.title"
            :cols="card.flex"
          >
            <v-card
              :loading="loading"
              class="mx-auto my-1"
              max-width="374"
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
                src="https://cdn.vuetifyjs.com/images/cards/cooking.png"
              ></v-img>
          
              <v-card-title v-text="card.name"></v-card-title>
              <v-divider class="mx-4"></v-divider>
          
              <v-card-title v-text="card.description"></v-card-title>
          
              Boxes:
              <v-card-actions>
                <v-btn
                  color="deep-purple lighten-2"
                  text
                  v-text="card.numberOfBoxes"
                  @click="reserve"
                >
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
  </v-app>
</template>

<script>

import axios from 'axios';

export default {
  name: 'App',

  data: () => ({
    loading: false,
    selection: 1,
    cards: [],
  }),
  mounted () {
  
    axios
      .get('http://192.168.1.226:8080/api/location')
      .then(response => {
        this.cards = response.data;
        console.log(response.data);
        })
  },
  methods: {
    
    reserve () {
      this.loading = true

      setTimeout(() => (this.loading = false), 2000)
    },
  },
};
</script>
