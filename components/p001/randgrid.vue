<template>
  <div class="rand-grid">
    <h1>randGrid</h1>
    <!-- <p>{{ gridState }}</p> -->
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
                v-for="(obj, index) in generatedDivs"
                :key="index"
                :style="{ backgroundColor: obj.color }"
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
            <h4>Orientation: {{ gridState.orientation }}</h4>
            <!-- radios for h v -->
            <v-radio-group v-model="gridState.orientation">
              <v-radio
                label="Horizontal"
                value="horizontal"
                checked="checked"
              ></v-radio
              ><v-radio label="Vertical" value="vertical"></v-radio>
            </v-radio-group>

            <h4>
              Dividers: {{ gridState.dividers }}
              <v-text-field
                variant="outlined"
                density="compact"
                v-model="gridState.dividers"
              ></v-text-field>
            </h4>

            <h4>Randomness:</h4>
            <br />
            <v-label>Size: {{ gridState.randomness.size }}</v-label>
            <v-slider
              v-model="gridState.randomness.size"
              min="0"
              max="10"
              step="1"
              >Size</v-slider
            >
            <v-label>Color: {{ gridState.randomness.color }}</v-label>
            <v-slider
              v-model="gridState.randomness.color"
              min="0"
              max="10"
              step="1"
              >Color</v-slider
            >

            <!-- sliders for size and color -->
          </v-card-text>

          <v-card-actions>
            <v-btn
              variant="tonal"
              type="submit"
              size="large"
              color="green"
              @click.prevent="handleRegenerate"
              >(RE)GENERATE</v-btn
            >
          </v-card-actions>
          <!-- </form> -->
        </v-card>
      </div>
    </div>
  </div>
</template>




<script>
export default {
  // name: "randGrid",
  data() {
    return {
      gridState: {
        orientation: "horizontal",
        randomness: {
          size: 0,
          color: 0,
        },
        dividers: 5,
      },
      regenerate: false,
      generatedDivs: [],
    };
  },
  computed: {
    gridOrientation() {
      if (this.gridState.orientation === "horizontal") {
        return "row";
      } else {
        return "column";
      }
    },
  },
  mounted() {
    this.generatedDivs = this.gridDivs();
  },
  watch: {
    regenerate() {
      this.generatedDivs = this.gridDivs();
    },
    gridState: {
      handler() {
        console.log("gridstate changed");
        this.generatedDivs = this.gridDivs();
      },
      deep: true,
    },
  },
  methods: {
    gridDivs() {
      let output = [];

      for (let i = 0; i < this.gridState.dividers; i++) {
        let obj = {
          size: Math.floor(Math.random() * this.gridState.randomness.size),
          color: this.randomColor(),
        };

        output.push(obj);
      }
      return output;
    },
    randomColor() {
      let baseColor = Math.floor(Math.random() * 255);

      let baseRemainder = 255 - baseColor;

      let r = Math.floor(Math.random() * 255) - baseRemainder;
      let g = Math.floor(Math.random() * 255) - baseRemainder;
      let b = Math.floor(Math.random() * 255) - baseRemainder;
      return `rgb(${r}, ${g}, ${b})`;
    },
    handleSubmit(e) {
      e.preventDefault();
      console.log("submit");
    },
    handleRegenerate() {
      this.regenerate = !this.regenerate;
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
