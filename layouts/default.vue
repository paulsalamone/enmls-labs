<template>
  <v-app>
    <!-- UTIL BAR -->
    <!-- <v-system-bar color="purple-darken-4
">
  <v-icon icon="mdi-wifi-strength-4"></v-icon>
  <v-icon icon="mdi-signal" class="ms-2"></v-icon>
  <v-icon icon="mdi-battery" class="ms-2"></v-icon>

  <span class="ms-2">3:13PM</span>
</v-system-bar> -->

<!-- MOBILE NAV -->
<!-- <v-app-bar :elevation="1">
    <v-icon icon="mdi-menu" class="ms-2"></v-icon>

  
  XP:   <v-icon icon="mdi-heart" class="ms-"></v-icon>
</v-app-bar> -->

<v-navigation-drawer color="blue" permanent location="left"  order="1" >
<v-list-item>1 yoooo</v-list-item>
<v-list-item>2 yoooo</v-list-item>
<v-list-item>yoooo</v-list-item>
<v-list-item>yoooo</v-list-item>

</v-navigation-drawer>
<!-- SIDEBAR NAV: temporary for when ENMLS is just for experiments -->
    
    <NuxtPage order="2" />

    <!-- permanent footer -->
  </v-app>
</template>