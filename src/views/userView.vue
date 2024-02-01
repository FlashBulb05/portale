<template>
  <v-container>
    <v-row>
      <v-col v-for="(ut, index) in this.utenti" :key="ut.id" cols="12" md="6" lg="3">
        <v-card class="mx-auto" max-width="344">
          <v-img :src="ut.image" height="200px" cover></v-img>

          <v-card-title>
            {{ ut.firstName }} {{ ut.lastName }}
          </v-card-title>

          <v-card-subtitle>
            {{ ut.email }}
          </v-card-subtitle>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn :icon="selectedCard === index ? 'mdi-chevron-up' : 'mdi-chevron-down'" @click="toggleCard(index)"></v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="selectedCard === index">
              <v-divider></v-divider>

              <v-card-text>
                <v-row>
                  <v-col cols="12" md="6">
                    <div>Data di nascita:</div>
                    <div>Età:</div>
                    <div>Sesso:</div>
                    <div>Numero di telefono:</div>
                  </v-col>
                  <v-col cols="12" md="6">
                    <div>{{ ut.birthDate }}</div>
                    <div>{{ ut.age }}</div>
                    <div>{{ ut.gender }}</div>
                    <div>{{ ut.phone }}</div>
                  </v-col>
                </v-row>
              </v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ut from "../utenti";

export default {
  name: 'HomeView',
  data() {
    return {
      selectedCard: null,
      prodotti: [],
      utenti: [],
      loading: false,
      selection: 1,
      downloaded: false,
    }
  },
  methods: {
    getProdotti() {
      fetch('https://dummyjson.com/products')
        .then(res => res.json())
        .then(console.log);
    },
    selectCard(index) {
      this.selectedCard = this.selectedCard === index ? null : index;
    },
    toggleCard(index) {
      this.selectedCard = this.selectedCard === index ? null : index;
    }
  },
  mounted() {
    this.utenti = ut;
  }
}
</script>
