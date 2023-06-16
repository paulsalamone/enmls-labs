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