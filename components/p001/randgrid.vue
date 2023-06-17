<template>
  <div class="rand-grid">
    <h1>randGrid</h1>

    <div class="app-grid">
      <div class="grids-output">
        <div class="grid-result">
          <!-- result itself -->
          <div class="grid-result-image"></div>
          <!-- button utils -->
          <div class="grid-result-buttons">
            <v-btn variant="tonal">save</v-btn><v-btn>refresh</v-btn>
          </div>
        </div>
      </div>

      <div class="grids-utils">
        <v-card variant="tonal">
          <v-card-item>
            <v-card-title> Grid Utils </v-card-title>
          </v-card-item>
          <v-divider></v-divider>
          <v-card-text>
            <h4>Orientation</h4>
            <!-- radios for h v -->
            <v-radio-group>
              <v-radio label="Vertical" value="vertical"></v-radio>
              <v-radio label="Horizontal" value="horizonal"></v-radio>
            </v-radio-group>
            <h4>Randomness:</h4>
            <p>Size</p>
            <v-slider>Size</v-slider>
            <p>Color</p>

            <v-slider>Color</v-slider>

            <!-- sliders for size and color -->
          </v-card-text>

          <v-card-actions>
            <v-btn variant="tonal">GENERATE</v-btn>
          </v-card-actions>
        </v-card>
      </div>
    </div>
  </div>
</template>


<script>
export default {};
</script>

<style scoped lang="scss">
.rand-grid {
  /* border: 2px solid black; */
  width: 100%;
  height: auto; /* updated */
}
.app-grid {
  display: grid;
  grid-template-columns: 3fr 2fr;
  /* border: 2px solid black; */
  width: 100%;
  height: auto; /* updated */
}

.grids-output {
}

.grid-result {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100%;
  width: 100%;
  padding: 1rem;
}

.grid-result-image {
  border: 4px solid black;
  height: 400px;
  width: 400px;
  margin: 1rem;
}
.grid-result-buttons {
  display: flex;

  button {
    margin: 0.25rem 0.5rem;
  }
}

.grids-utils {
  padding: 1rem;
}
</style>
