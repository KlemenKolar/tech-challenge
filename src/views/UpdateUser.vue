<template>
    <h1>Update user information</h1>
    <p>The API doesn't actually update the information!</p>
    <v-divider class="border-opacity-25" color="success" :thickness="4"></v-divider>
    <v-sheet width="300" class="mx-auto" height="500">
    <v-form @submit.prevent="updateInfo" class="updateForm">
      <v-text-field
        v-model="firstName"
        label="First name"
      ></v-text-field>
      <v-text-field
        v-model="lastName"
        label="Last name"
        
      ></v-text-field>
      <v-text-field
        v-model="telephone"
        label="Telephone number"
        
      ></v-text-field>
      <v-btn type="submit" block class="mt-2">Submit</v-btn>
    </v-form>
  </v-sheet>
</template>

<script>
import router from '@/router';

export default {
  data() {
    return {
      firstName: this.$route.query.firstName,
      lastName: this.$route.query.lastName,
      telephone: this.$route.query.telephone,
    };
  },
  methods: {
      updateInfo(){
        fetch('https://dummyjson.com/users/1', {
        method: 'PUT',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            firstName: this.firstName,
            lastName: this.lastName,
            phone: this.telephone
        })
        })
        .then(res => res.json())
        .then(console.log);
        router.push({path: "/users"})
      },
    },
}
</script>

<style>
.updateForm {
    padding: 20px
}
h1 {
  text-align: center;
}
p {
    text-align: center;
}
</style>