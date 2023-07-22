<template>
    <h1>Products</h1>
    <v-card-text>
      <v-text-field
        type="text"
        v-model="search"
        density="compact"
        variant="solo"
        label="Search products"
        append-inner-icon="mdi-magnify"
        single-line
        hide-details
        @click:append-inner="filteredProducts"
        @input="filteredProducts"
      ></v-text-field>
    </v-card-text>
    <v-divider class="border-opacity-25" color="success" :thickness="4"></v-divider>
      <v-container>
        <v-row>
          <v-col
            v-for="item in items.products"
            key="12"
            cols="12"
            md="4"
          >
            <v-sheet
              class="pa-12"
              color="grey-lighten-3"
              :title=item.title
              height="400px"
            >
            <div class="d-flex justify-center" :id="item.id">
              <v-card width="300px">
                <v-card-title class="font-weight-medium">{{ item.title }}</v-card-title>
                <v-card-text>
                  <img :src="item.thumbnail" class="image"/>
                </v-card-text>
              </v-card>
            </div>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>
    </template>
    
    <script>
    export default {
        data() {
            return {
            items: [],
            search: "",
            };
        },
        mounted() {
        fetch('https://dummyjson.com/products')
            .then(response => response.json())
            .then(data => {
            this.items = data;
            console.log(data)
            })
            .catch(error => {
            console.error(error);
            });
        },
        methods: {
            filteredProducts(){
                console.log(this.search);
                fetch('https://dummyjson.com/products/search?q=' + this.search)
                .then(response => response.json())
                .then(data => {
                this.items = data;
                console.log(data)
                })
                .catch(error => {
                console.error(error);
                })
            },
        },
    }
    
    </script>
    
    <style>
    h1 {
      text-align: center;
    }
    
    .image {
      max-width: 100%;
      max-height: 100%;
      width: auto;
      height: auto;
    }
    </style>