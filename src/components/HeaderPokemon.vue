<template>
  <q-header elevated class="bg-white text-grey-8">
    <q-img src="../assets/fundo.jpg" class="header-image absolute-top" />
    <div class="column" id="header">
      <div class="col self-center">
        <q-avatar square id="logo">
          <img src="../assets/Pokemon-Logo.png" />
        </q-avatar>
      </div>
    </div>
  </q-header>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "HeaderPokemon",
});
</script>

<style lang="scss">
#header {
  padding: 10px 0px;
  height: 16rem;
  margin: auto;
}
.bg-grey-1 {
  min-height: 260px !important;
}
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 1.3;
  filter: grayscale(50%);
}
#search {
  background-color: beige;
}
#logo {
  width: 18rem;
  height: 9rem;
}
</style>
