<template>
  <div class="rand-grid">
    <h1>randGrid</h1>
    <!-- <p>{{ gridState }}</p> -->
    <div class="app-grid">
      <v-sheet elevation="4">
        <div class="grids-output">
          <div class="grid-result">
            <!-- result itself -->
            <div class="grid-result-image" :style="{ flexDirection: gridType }">
              <!-- GRID IMAGE -->
              <div
                class="divider grid-cell"
                v-for="(obj, index) in generatedDivs"
                :key="index"
                :style="{
                  backgroundColor: obj.color,
                  color: 'white',
                  height: gridType === 'row' ? '100%' : `${obj.size}%`,
                  width: gridType === 'row' ? `${obj.size}%` : '100%',
                }"
              >
                <!-- vertical is going to be a row of shit -->
                <!-- horizontal is going to be a column of shit -->
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
            <h4>Type: {{ gridState.type }}</h4>
            <!-- radios for h v -->
            <v-radio-group v-model="gridState.type">
              <v-radio
                label="Horizontal"
                value="horizontal"
                checked="checked"
              ></v-radio
              ><v-radio label="Vertical" value="vertical"></v-radio>
            </v-radio-group>

            <h4>
              Dividers: {{ dividers - 1 }}
              <v-slider v-model="dividers" min="2" max="100" step="1"
                >Size</v-slider
              >

              <!-- <v-text-field
                variant="outlined"
                density="compact"
                v-model="gridState.dividers"
              ></v-text-field> -->
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
              @click.prevent="handleRegenerateAll"
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
        type: "horizontal",
        randomness: {
          size: 0,
          color: 0,
        },
      },
      dividers: 5,

      regenerateAll: false,
      generatedDivs: [],
    };
  },
  computed: {
    gridType() {
      if (this.gridState.type === "horizontal") {
        return "row";
      } else {
        return "column";
      }
    },
  },
  mounted() {
    this.generatedDivs = this.getDivs();
    // this.getRandomSizes();
  },
  watch: {
    regenerateAll() {
      this.generatedDivs = this.getDivs();
    },
    dividers() {
      this.generatedDivs = this.getDivs();
    },
    // gridState: {
    //   handler() {
    //     console.log("gridstate changed");
    //     this.generatedDivs = this.getDivs();
    //   },
    //   deep: true,
    // },
  },
  methods: {
    getSizeStyle(index) {
      return `height: ${this.generatedDivs[index].size}%;`;
      // if (this.gridState.type === "horizontal") {
      //   return "h-" + this.generatedDivs[index].size;
      // } else {
      //   return "v-" + this.generatedDivs[index].size;
      // }
    },
    getRandomSizes() {
      const output = [];
      let sum = 0;

      for (let i = 0; i < this.dividers; i++) {
        const remaining = 100 - sum;

        // Calculate maximum size based on number of dividers left
        const maxDividersLeft = this.dividers - i;
        const maxSize = Math.min(
          remaining,
          1 + Math.floor((remaining - maxDividersLeft) / maxDividersLeft)
        );

        const nextSize = Math.floor(Math.random() * maxSize) + 1;
        sum += nextSize;

        // Ensure last cell completes to 100%
        if (i === this.dividers - 1) {
          output.push(100 - sum + nextSize);
        } else {
          output.push(nextSize);
        }
      }

      return output;
    },
    getDivs() {
      let output = [];

      for (let i = 0; i < this.dividers; i++) {
        let obj = {
          // size: Math.floor(Math.random() * this.gridState.randomness.size),
          color: this.randomColor(),
        };

        output.push(obj);
      }

      const sizes = this.getRandomSizes();
      console.log(sizes);
      output.forEach((el, index) => {
        el.size = sizes[index];
      });
      console.log(output);
      return output;
    },
    randomColor() {
      const hue = Math.floor(Math.random() * 360);
      const saturation = Math.floor(Math.random() * 101) + "%";
      const lightness = Math.floor(Math.random() * 101) + "%";
      return `hsl(${hue}, ${saturation}, ${lightness})`;
    },
    handleSubmit(e) {
      e.preventDefault();
      console.log("submit");
    },
    handleRegenerateAll() {
      this.regenerateAll = !this.regenerateAll;
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

.grid-cell {
  // border: 0.5px dotted grey;
  width: 100%;
  height: 100%;
}
.grids-utils {
  padding: 1rem;
}
</style>
