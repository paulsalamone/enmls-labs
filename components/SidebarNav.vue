<template>
  <div>
    <nav class="layout-nav">
      <!-- MOBILE NAV HERE? -->
      <!-- <v-app-bar-nav-icon /> -->
      <!-- <v-app-bar-title> EMNLS </v-app-bar-title> -->

      <NuxtLink to="/"> <h1 class="logo">ENMLS</h1></NuxtLink>
      <NuxtLink to="p001_randbox">
        <v-list-item prepend-icon="mdi-view-dashboard">
          randGrid</v-list-item
        ></NuxtLink
      >
      <v-list-item prepend-icon="mdi-account-box" title="Account"></v-list-item>
      <v-list-item prepend-icon="mdi-gavel" title="Admin"></v-list-item>
    </nav>
  </div>
</template>

<style lang="scss">
.layout-nav {
  height: 100%;
  width: 300px;
  width: fit-content;
  padding: 1rem;
  background-color: darkgrey;
  height: 100vh;
  border: 2px solid purple;

  a {
    text-decoration: none;
    color: black;
  }
}</style>