<template>
  <v-app class="layout-page">
    <div class="layout-content">
      <SidebarNav class="layout-nav" />
      <v-main class="layout-main">
        <!-- <TopBar /> -->
        <NuxtPage />
      </v-main>
    </div>

    <Footer class="layout-footer" />
  </v-app>
</template>

<style lang="scss">
.layout-page {
  display: flex;
  flex-direction: column;
  align-items: space-between;
  height: 100%;
  /* border: 20px solid black; */
}

.layout-content {
  /* border: 10px solid red; */
  display: flex;
  flex-direction: row;
  height: 100%;
  min-height: 100vh;
}

.layout-nav {
  height: 100%;
  width: 200px;
  width: fit-content;
  padding: 1rem;
  background-color: darkgrey;
  height: 100vh;

  a {
    text-decoration: none;
    color: black;
  }
}

.layout-footer {
  position: absolute;
  bottom: -20px;
  background-color: black;
  color: white;
  width: 100vw;
}

.layout-main {
  margin: 3rem 1.5rem;
}

h1,
h2 {
  margin-bottom: 1.5rem;
}
</style>