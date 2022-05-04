<template>
  <div class="column items-center">
    <div class="col" id="container-perfil">
      <div class="text-h4" id="title">{{ pokemonName }}</div>

      <q-avatar id="avatar">
        <img :src="pokemon.image" />
      </q-avatar>
      <div
        style="display: flex; justify-content: center"
        v-for="(type, index) in pokemon.types"
        :key="index"
      >
        <p style="font-size: 18px" id="tipos">{{ type.type.name }}</p>
      </div>
      <p id="data">Peso: {{ pokemon.weight }}kg</p>
      <p id="data">Altura: {{ pokemon.height }}m</p>
      <p id="data" v-for="(stat, index) in pokemon.stats" :key="index">
        {{ stat.stat.name }}: {{ stat.base_stat }}
      </p>
      <q-btn
        style="background: goldenrod; color: white"
        glossy
        label="Voltar"
        id="button-back"
        @click="goBack"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonPage",

  props: ["pokemonName"],
  data() {
    return {
      pokemon: {
        image: "",
        types: [],
        height: Number,
        weight: Number,
        stats: [],
      },
    };
  },
  created: function () {
    this.$api.get(`pokemon/${this.pokemonName}`).then((response) => {
      this.pokemon.image = response.data.sprites.front_default;
      this.pokemon.types = response.data.types;
      this.pokemon.weight = (response.data.weight * 0.453592).toFixed(1);
      this.pokemon.height = (response.data.height / 10).toFixed(1);
      this.pokemon.stats = response.data.stats;
      console.log(this.pokemon.stats);
    });
  },
  methods: {
    goBack: function () {
      this.$router.push({ path: `/` });
    },
  },
};
</script>
<style>
#avatar {
  width: 10rem;
  height: 10rem;
  box-shadow: 0px 0px 1em gold;
  margin: 45px 0px;
}
#data {
  text-align: center;
  text-transform: capitalize;
  font-size: 18px;
}
#title {
  text-transform: capitalize;
  text-align: center;
}
#container-perfil {
  width: 20rem;
  margin: 2rem;
  box-shadow: 0px 0px 1em gold;
  border-radius: 2rem;
  padding: 1.5rem;
}
#button-back,
#container-perfil,
#data,
#avatar {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
</style>
