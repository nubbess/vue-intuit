<template>
  <NavbarComponent nombre-web="IntuitWeather"/>
  <div class="container">
    <div class="sapo">
      <SearchEngine class=""/>
    </div>
  </div>
</template>

<script setup>
  import NavbarComponent from './components/nav/NavbarComponent.vue';
  import SearchEngine from './components/search_engine/SearchEngine.vue';
</script>

<style>
  .sapo {
    display: flex;
    padding: 10px
  }
</style>