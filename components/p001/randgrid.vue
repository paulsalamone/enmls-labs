<template>
  <div class="rand-grid">
    <h1>randGrid {{ gridOrientation }}</h1>

    <div class="app-grid">
      <v-sheet elevation="4">
        <div class="grids-output">
          <div class="grid-result">
            <!-- result itself -->
            <div
              class="grid-result-image"
              :style="{ flexDirection: gridOrientation }"
            >
              <!-- GRID IMAGE -->
              <div
                class="divider"
                v-for="(obj, index) in gridDivs"
                :key="index"
              >
                <!-- {{ obj }} -->
              </div>
            </div>
            <!-- button utils -->
            <div class="grid-result-buttons">
              <v-btn prepend-icon="mdi-wiper" variant="tonal">clear</v-btn
              ><v-btn prepend-icon="mdi-content-save">save</v-btn>
            </div>
          </div>
        </div>
      </v-sheet>
      <div class="grids-utils">
        <v-card elevation="0">
          <!-- <form action="" @submit="handleSubmit"> -->
          <v-card-item>
            <v-card-title> Grid Utils </v-card-title>
          </v-card-item>
          <v-divider></v-divider>

          <v-card-text>
            <h4>Orientation: {{ orientation }}</h4>
            <!-- radios for h v -->
            <v-radio-group v-model="orientation">
              <v-radio
                label="Horizontal"
                value="horizontal"
                checked="checked"
              ></v-radio
              ><v-radio label="Vertical" value="vertical"></v-radio>
            </v-radio-group>

            <h4>
              Dividers: {{ dividers }}
              <v-text-field
                variant="outlined"
                density="compact"
                v-model="dividers"
              ></v-text-field>
            </h4>

            <h4>Randomness:</h4>
            <br />
            <v-label>Size: {{ randomness.size }}</v-label>
            <v-slider v-model="randomness.size" min="0" max="10" step="1"
              >Size</v-slider
            >
            <v-label>Color: {{ randomness.color }}</v-label>
            <v-slider v-model="randomness.color" min="0" max="10" step="1"
              >Color</v-slider
            >

            <!-- sliders for size and color -->
          </v-card-text>

          <!-- <v-card-actions>
              <v-btn variant="tonal" type="submit" size="large" color="green"
                >(RE)GENERATE</v-btn
              >
            </v-card-actions> -->
          <!-- </form> -->
        </v-card>
      </div>
    </div>
  </div>
</template>




<script>
export default {
  name: "randGrid",
  data() {
    return {
      orientation: "horizontal",
      randomness: {
        size: 0,
        color: 0,
      },
      dividers: 5,
    };
  },
  computed: {
    gridOrientation() {
      if (this.orientation === "horizontal") {
        return "row";
      } else {
        return "column";
      }
    },
    gridDivs() {
      let output = [];
      for (let i = 0; i < this.dividers; i++) {
        let obj = {
          size: Math.floor(Math.random() * this.randomness.size),
          color: Math.floor(Math.random() * this.randomness.color),
        };
        output.push(obj);
      }
      return output;
    },
  },
  methods: {
    handleSubmit(e) {
      e.preventDefault();
      console.log("submit");
    },
  },
};
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
  display: flex;
  justify-content: space-between;
  align-items: space-between;
}

.divider {
  border: 1px dotted grey;
  height: 100%;
  width: 100%;
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
