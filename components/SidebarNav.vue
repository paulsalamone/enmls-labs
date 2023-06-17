<template>
  <div>
    <nav class="layout-nav">
      <!-- MOBILE NAV HERE? -->
      <!-- <v-app-bar-nav-icon /> -->
      <!-- <v-app-bar-title> EMNLS </v-app-bar-title> -->

      <NuxtLink to="/"> <h1 class="logo">ENMLS</h1></NuxtLink>
      <NuxtLink to="p001_randgrid">
        <v-list-item prepend-icon="mdi-view-dashboard">
          randGrid</v-list-item
        ></NuxtLink
      >
    </nav>
  </div>
</template>

<style lang="scss">
.logo {
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  font-size: 3rem;
  letter-spacing: -2px;
}
</style>