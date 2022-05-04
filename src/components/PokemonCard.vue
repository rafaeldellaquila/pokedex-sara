<template>
  <q-card class="my-content" :id="pokemon.name" :ref="pokemon.name">
    <q-img :src="pokemon.image" id="imagem-pokemon" decoding="async" />
    <q-card-section
      class="absolute-bottom text-subtitle3 text-center"
      id="pokemon-name"
    >
      <h2 class="text-title">{{ this.name }}</h2>
      <div
        class="text-subtitle1"
        style="display: flex; justify-content: center"
      >
        <p
          v-for="type in types"
          :key="type.type.name"
          id="tipos"
          style="text-transform: capitalize"
        >
          {{ type.type.name }}
        </p>
      </div>
    </q-card-section>
  </q-card>
</template>

<script>
export default {
  name: "PokemonCard",
  data() {
    return {
      pokemon: {
        image: "",
        name: "",
      },
      types: [],
    };
  },

  props: {
    name: String,
    url: String,
  },

  created: function () {
    this.$axios.get(this.url).then((response) => {
      this.pokemon.types = response.data.types;
      this.pokemon.image = response.data.sprites.front_default;
      this.pokemon.name = response.data.name;
    });
  },
};
</script>

<style>
#pokemon-name {
  font-size: 20px;
  text-transform: capitalize;
  padding: 5px;
  height: 10vh;
}
.my-content {
  width: 18rem !important;
}
#tipos {
  padding-right: 5px;
  font-size: 15px;
  text-transform: capitalize;
}
</style>
