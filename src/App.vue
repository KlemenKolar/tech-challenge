<template>
<v-card>
    <v-layout>
      <v-navigation-drawer
        expand-on-hover
        rail
      >
        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-account-group" title="Users" value="Users" to="/users"></v-list-item>
          <v-list-item prepend-icon="mdi-cart-variant" title="Carts" value="Carts" to="/carts"></v-list-item>
          <v-list-item prepend-icon="mdi-star" title="Products" value="Products" to="/products"></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-main>
        <router-view></router-view>
      </v-main>
    </v-layout>
  </v-card>
</template>

<script setup>
  import { ref } from 'vue'

  const drawer = ref(null)
</script>

<script>
  export default {
    data: () => ({ drawer: null }),
  }
</script>