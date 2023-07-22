<template>
    <h1>Users</h1>
    <v-card-text>
      <v-text-field
        type="text"
        v-model="search"
        density="compact"
        variant="solo"
        label="Search users"
        append-inner-icon="mdi-magnify"
        single-line
        hide-details
        @click:append-inner="filteredUsers"
        @input="filteredUsers"
      ></v-text-field>
    </v-card-text>
  <v-divider class="border-opacity-25" color="success" :thickness="4"></v-divider>
    <v-container>
      <v-row>
        <v-col
          v-for="item in items.users"
          :key="item.id"
          cols="12"
          md="4"
        >
          <v-sheet
            class="pa-12"
            color="grey-lighten-3"
            :title=item.title
            height="450px"
          >
          <div class="d-flex justify-center" :id="item.id">
            <v-card width="300px">
              <v-card-title class="font-weight-medium">{{ item.firstName + " " + item.lastName }}</v-card-title>
              <v-card-text>
                <img :src="item.image" class="image"/>
              </v-card-text>
            </v-card>
          </div>
          <div class="button-container">
          <v-btn
          float="left"
          class="left-button"
          color="primary"
          @click="toggleExpand(item.id)"
        >
          More info
        </v-btn>
        <v-btn
          color="primary"
          :to="{path:'/updateuser',query:{id: item.id, firstName: item.firstName, lastName: item.lastName, telephone: item.phone}}"
        >
          Update user info
        </v-btn>
      </div>
        <v-expand-transition>
          <v-card v-if="isExpanded(item.id)" 
            height="200"
            width="200"
            z-index="9999"
            class="overlay">
          <b>Age: {{ item.age }}</b><br>
          <b>Email: {{ item.email }}</b><br>
          <b>Gender: {{ item.gender }}</b><br>
          <b>Phone: {{ item.phone }}</b><br>
          <b>University: {{ item.university }}</b>
          </v-card>
        </v-expand-transition>
        <v-col class="shrink" >
      </v-col>
  
          </v-sheet>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  import router from '@/router';
  
    export default {
        data() {
            return {
            items: [],
            expandedStates: Array.from(100, () => false),
            search: "",
            };
        },
        mounted() {
        fetch('https://dummyjson.com/users')
            .then(response => response.json())
            .then(data => {
            this.items = data;
            console.log(data)
            })
            .catch(error => {
            console.error(error);
            })
        },
        methods: {
            filteredUsers(){
                console.log(this.search);
                fetch('https://dummyjson.com/users/search?q=' + this.search)
                .then(response => response.json())
                .then(data => {
                this.items = data;
                console.log(data)
                })
                .catch(error => {
                console.error(error);
                })
            },
            toggleExpand(id){
                console.log(id);
                this.expandedStates[id] = !this.expandedStates[id];
            },
            isExpanded(index) {
            return this.expandedStates[index] === true;
            },
            },
    }
  </script>
  
  <style>
  .overlay {
    position: absolute;
    padding: 10px;
    width: 100%;
    height: 100%;
    background-color: rgb(255, 255, 255);
    z-index: 9999;
  }
  
  h1 {
    text-align: center;
  }
  
  .image {
    max-width: 80%;
    max-height: 80%;
    width: auto;
    height: auto;
  }
  .button-container {
    display: flex;
    padding: 10px;
  }
  
  .left-button {
    margin-right: 10px; /* Adjust the spacing between buttons as needed */
  }
  
  .delete-button {
    margin-left: 200px;
    margin: 10px;
  }
  </style>
  