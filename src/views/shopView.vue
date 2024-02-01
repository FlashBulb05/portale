<template>
     <div class="shop">
    <h1>Shop prodotti</h1>

    
    </div>
  
    <v-card flat class="text-left">
    <v-card-title class="d-flex align-center pe-2">
      PRODOTTI

      <v-spacer></v-spacer>
    </v-card-title>

    <v-divider></v-divider>
    <v-data-table :items="prodotti">

      <template v-slot:[`item.image`]="{ item }">
        <v-card class="my-2" elevation="2" rounded>
          <v-img
            :src="`${item.image}`"
            height="64"
            cover
          ></v-img>
        </v-card>
      </template>

      <template v-slot:[`item.rating`]="{ item }">
        <v-rating
          :model-value="item.rating.rate"
          color="orange-darken-2"
          density="compact"
          size="small"
          readonly
        ></v-rating>
      </template>

      <template v-slot:[`item.category`]="{ item }">
        <div class="text-end">
          <v-chip
            :text="item.category"
          ></v-chip>
        </div>
      </template>
    </v-data-table>
  </v-card>
  </template>
  <script>

  export default {
    /* eslint-disable */
    name: 'Shop',
    data() {
      return {
        prodotti: [],
        loading: false,
        selection: 1,
        downloaded: false,
      }
    },
    methods: {
      getProdotti() {
        if(!localStorage.getItem('prodotti')){
          fetch('https://fakestoreapi.com/products')
                  .then(res => res.json())
                  .then(json => {
                    this.prodotti = json;
                    this.prodotti.forEach((item) => {
                      item.quantity = Math.floor(Math.random()*100) + 1;
                    })
                    localStorage.setItem('prodotti', JSON.stringify(this.prodotti))
                    console.log("Products: ", this.prodotti)
                    console.log("STORAGEEEE")
                    console.log(JSON.parse(localStorage.getItem('prodotti')))
                  })
        }else{
          console.log("Almost downloaded...")
          this.prodotti = JSON.parse(localStorage.getItem('prodotti'))
          console.log(JSON.parse(localStorage.getItem('prodotti')))
        }
        
      }
    },
    mounted() {
      this.getProdotti()
    }
  }
  </script>
  
  