<template>
  <div class="rand-grid">
    <h1>randGrid</h1>
    <p>r color:{{ randomColor }}</p>
    <div class="app-grid">
      <v-sheet elevation="4">
        <!-- CONVERT TO COMPONENT -->
        <div class="grids-output">
          <div class="grid-result">
            <div
              class="grid-result-image"
              :style="{
                display: gridType !== 'full' ? 'flex' : 'grid',
                flexDirection: gridType !== 'full' ? gridType : null,
                gridTemplateRows: gridType === 'full' ? gridRowsFRs : null,
                gridTemplateColumns:
                  gridType === 'full' ? gridColumnsFRs : null,
              }"
            >
              <div
                class="divider grid-cell"
                v-for="(obj, index) in gridObjects"
                :key="index"
                :style="{
                  backgroundColor: obj.color,
                  height:
                    this.gridType === 'full'
                      ? '100%'
                      : this.gridType === 'row'
                      ? '100%'
                      : `${obj.size}%`,
                  width:
                    this.gridType === 'full'
                      ? '100%'
                      : this.gridType === 'row'
                      ? `${obj.size}%`
                      : '100%',
                }"
              ></div>
            </div>

            <!-- ADD NAMER!!! -->

            <!-- button utils -->
            <div class="grid-result-buttons">
              <v-btn prepend-icon="mdi-wiper" variant="tonal">clear</v-btn
              ><v-btn prepend-icon="mdi-content-save">save</v-btn>
            </div>
          </div>
        </div>
      </v-sheet>
      <!-- CONVERT TO COMPONENT: GridUtils -->
      <div class="grids-utils">
        <v-card elevation="0">
          <v-card-item>
            <v-card-title> Grid Utils </v-card-title>
          </v-card-item>
          <v-divider></v-divider>
          <v-card-text>
            <h4>Type: {{ gridTypeSelector }}</h4>
            <v-radio-group v-model="gridTypeSelector">
              <v-radio
                label="Horizontal"
                value="horizontal"
                checked="checked"
              ></v-radio
              ><v-radio label="Vertical" value="vertical"></v-radio>
              <v-radio label="Full" value="full"></v-radio>
            </v-radio-group>
            <h4>
              Dividers: {{ dividers - 1 }}
              <v-slider v-model="dividers" min="2" max="100" step="1"
                >Size</v-slider
              >
            </h4>

            <h4>Randomness:</h4>
            <br />
            <v-label>Color: {{ randomColor }}</v-label>
            <v-slider v-model="randomColor" min="0" max="50" step="1"
              >Color</v-slider
            >
            <v-label>Size: {{ gridState.randomness.size }}</v-label>
            <v-slider
              v-model="gridState.randomness.size"
              min="0"
              max="10"
              step="1"
              >Size</v-slider
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
      gridTypeSelector: "horizontal",
      gridState: {
        randomness: {
          size: 5,
          color: 5,
        },
      },
      randomColor: 5,
      dividers: 5,
      sizesList: [],
      gridObjects: [],
      regenerateAll: false,
      gridColumnsFRs: "",
      gridRowsFRs: "",
    };
  },
  computed: {
    gridType() {
      if (this.gridTypeSelector === "horizontal") {
        return "column";
      } else if (this.gridTypeSelector === "vertical") {
        return "row";
      } else {
        return "full";
      }
    },
    fulLGridNumber() {
      return this.dividers * this.dividers;
    },
  },
  mounted() {
    this.gridObjects = this.getGridObjects();
  },
  watch: {
    regenerateAll() {
      this.gridObjects = this.getGridObjects();
    },
    dividers(val) {
      console.log("dividers watcher:", val);
      this.gridObjects = this.getGridObjects();
    },
    gridTypeSelector(val) {
      console.log("gridTypeSelector: ", val);
      if (val === "full") {
        this.gridObjects = this.getGridObjects();
      }
    },
    randomColor(val) {
      this.gridObjects = this.getGridObjects();
    },
    sizesList(val) {
      console.log("sizesList", val);
    },
  },
  methods: {
    getDimension(orientation) {
      if (this.gridType === "full") {
        return null;
      } else if (orientation === "height") {
        this.gridType === "row" ? "100%" : `${obj.size}%`;
      } else {
        this.gridType === "row" ? `${obj.size}%` : "100%";
      }
    },

    getGridObjects() {
      let output = [];

      // will get number of dividers and generate random sizes
      const totalDivisions =
        this.gridTypeSelector !== "full" ? this.dividers : this.fulLGridNumber;

      this.sizesList = this.getRandomSizes();

      const startingHue = Math.floor(Math.random() * 360);
      const startingSaturation = Math.floor(Math.random() * 100);
      const startingLightness = Math.floor(Math.random() * 100);
      console.log(totalDivisions);

      for (let i = 0; i < totalDivisions; i++) {
        let obj = {
          color: this.getRandomColor(
            startingHue,
            startingSaturation,
            startingLightness
          ),
        };

        output.push(obj);
      }

      output.forEach((el, index) => {
        el.size = this.sizesList[index];
      });

      console.log(output);
      return output;
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

      // Shuffle the output array using Fisher-Yates algorithm
      for (let i = output.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [output[i], output[j]] = [output[j], output[i]];
      }

      this.gridColumnsFRs = output.map((el) => el + "fr").join(" ");

      for (let i = output.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [output[i], output[j]] = [output[j], output[i]];
      }

      this.gridRowsFRs = output.map((el) => el + "fr").join(" ");
      return output;
    },
    flipCoin(coin) {
      // coin flip

      const randomNumber = Math.random();
      if (randomNumber < 0.5) {
        coin = -coin;
      } else {
        coin = coin;
      }

      return coin;
    },
    getRandomNumber(min, max) {
      const randomNumber = Math.random();

      const scaledRandomNumber = randomNumber * (max - min + 1);

      const shiftedRandomNumber = scaledRandomNumber + min;

      const finalRandomNumber = Math.floor(shiftedRandomNumber);

      return finalRandomNumber;
    },

    getRandomColor(startingHue, startingSaturation, startingLightness) {
      const hue = Math.abs(
        startingHue +
          this.flipCoin(this.randomColor + this.getRandomNumber(0, 10))
      );
      const saturation =
        Math.abs(
          startingSaturation +
            this.flipCoin(
              this.getRandomNumber(
                0,
                100 - startingSaturation + this.randomColor
              )
            )
        ) + "%";
      const lightness =
        Math.abs(
          startingLightness +
            this.flipCoin(
              this.getRandomNumber(
                0,
                100 - startingLightness + this.randomColor
              )
            )
        ) + "%";

      console.log(`hsl(${hue}, ${saturation}, ${lightness})`);
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
