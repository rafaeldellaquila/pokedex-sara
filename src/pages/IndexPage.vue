<template>
  <q-page class="flex flex-center">
    <section class="full-width">
      <q-input
        v-model="searchValue"
        debounce="500"
        filled
        placeholder="Buscar Pokemon..."
        style="background-color: beige; border-radius: 8px"
      >
        <template v-slot:append>
          <q-icon name="search" />
        </template>
      </q-input>
      <q-select v-model="type" :options="types" label="Elemento do Pokemon" />
    </section>
    <div class="flex">
      <div v-for="pokemon in searchResults" :key="pokemon.name">
        <PokemonCard
          :name="pokemon.name"
          :url="pokemon.url"
          @click="handleClick(pokemon.name)"
        />
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import PokemonCard from "src/components/PokemonCard.vue";

export default defineComponent({
  name: "IndexPage",

  components: {
    PokemonCard,
  },

  data() {
    return {
      searchValue: "",
      pokemons: [],
      type: "",
      types: [
        {
          value: "",
          label: "All",
        },
      ],
    };
  },

  created: function () {
    this.$api("/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
      })
      .catch((err) => {
        console.log(err);
      });

    this.$api.get("type").then((response) => {
      response.data.results.forEach((type) => {
        // console.log(type);
        this.types.push(type);
      });
      //console.log(this.types);
    });
  },

  computed: {
    searchResults() {
      let filteredPokemons = this.pokemons;

      if (this.searchValue != " " && this.searchValue)
        filteredPokemons = filteredPokemons.filter((pokemon) => {
          return pokemon.name.toLowerCase().includes(this.searchValue);
        });
      return filteredPokemons;
    },
  },

  methods: {
    handleClick(pokemonName) {
      console.log(pokemonName);

      this.$router.push({
        name: "Pokemon",
        params: {
          pokemonName: pokemonName,
        },
      });
    },
  },
});
</script>
