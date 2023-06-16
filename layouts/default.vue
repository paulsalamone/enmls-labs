<template>
  <v-app class="layout-page">
    <div class="layout-content">
      <SidebarNav class="layout-nav" />
      <main>
        <!-- <TopBar /> -->
        <NuxtPage />
      </main>
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
  //   width: 200px;
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

main {
  padding: 1rem;
}
</style>