<template>
  <q-layout view="hHh lpR fFf">
    <headerPokemon />
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>
<script>
import HeaderPokemon from "../components/HeaderPokemon.vue";
export default {
  components: {
    HeaderPokemon,
  },
};
</script>
