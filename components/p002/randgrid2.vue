<template>
  <div class="rand-grid">
    <div class="app-grid">
      <v-sheet elevation="4">
        <!-- CONVERT TO COMPONENT -->
        <div class="grids-output">
          <div class="grid-result">
            <!-- META GRID -->
            {{ dividersHorizontal }}
            {{ dividersVertical }}
            <div
              class="grid-result-image"
              :style="{
                gridTemplateRows: rows,
                gridTemplateColumns: columns,
              }"
            >
              <!-- CELLS -->
              <div
                v-if="loaded"
                class="grid-cell"
                v-for="(cell, index) in cells"
                :key="index"
                :style="{
                  backgroundColor: cell.backgroundColor,
                  borderWidth: cell.borderWidth,
                  borderColor: cell.borderColor,
                  borderStyle: cell.borderStyle,
                }"
              >
                <!-- {{ cell }} -->
                <!-- {{ obj.radius }} -->
              </div>
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
            <!-- have locked option -->
            <h4>
              DIVIDERS:
              <v-checkbox v-model="dividersLocked" label="Locked"></v-checkbox>
            </h4>
            <h4>
              {{ dividersLocked ? "Divisions" : "Divisions Horizontal" }}:
              {{ dividersHorizontal - 1 }}
              <v-slider v-model="dividersHorizontal" min="1" max="50" step="1"
                >Size</v-slider
              >
            </h4>
            <h4 v-if="!dividersLocked">
              Dividers Vertical: {{ dividersVertical - 1 }}
              <v-slider v-model="dividersVertical" min="1" max="50" step="1"
                >Size</v-slider
              >
            </h4>

            <h4>Randomness:</h4>
            <br />
            <v-label>Color: {{ randomColor }}</v-label>
            <v-slider v-model="randomColor" min="0" max="50" step="1"
              >Color</v-slider
            >
            <v-label>Radius Range: {{ randomRadius }}</v-label>
            <v-slider v-model="randomRadius" min="0" max="50" step="1"
              >Size</v-slider
            >

            <!-- <v-label>Size: {{ gridState.randomness.size }}</v-label>
            <v-slider
              v-model="gridState.randomness.size"
              min="0"
              max="10"
              step="1"
              >Size</v-slider
            > -->

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
import meta from "./helpers/meta";

export default {
  data() {
    return {
      loaded: false,
      rows: "",
      columns: "",
      cells: [],
    };
  },
  mixins: [meta],
  computed: {
    cellAmount() {
      return this.dividersVertical * this.dividersHorizontal;
    },
  },
  mounted() {
    this.createInitialGrid();
    console.log("cells", this.cells);
  },
  watch: {
    // make a deep watcher here to monitor the entire grid? or is this better left to pinia?
    dividersHorizontal: function (newVal, oldVal) {
      if (newVal !== oldVal) {
        if (this.dividersLocked) {
          this.dividersVertical = newVal;
        }
        // perform update on horizontal dividers here
        this.createRowsColumns();
        this.createCells();
      }
    },
    dividersVertical: function (newVal, oldVal) {
      if (newVal !== oldVal) {
        // perform update on vertical dividers here
        this.createRowsColumns();
        this.createCells();
      }
    },
    dividersLocked(val) {
      if (val) {
        this.dividersVertical = this.dividersHorizontal;
      }
    },
  },
  methods: {
    createInitialGrid() {
      this.createRowsColumns();
      this.createCells();

      this.loaded = true;
    },
    createRowsColumns() {
      this.rows = `repeat(${this.dividersVertical}, 1fr)`;
      this.columns = `repeat(${this.dividersHorizontal}, 1fr)`;
    },
    createCells() {
      this.cells = [];
      for (let i = 0; i < this.cellAmount; i++) {
        this.cells.push({
          backgroundColor: "tan",
          borderColor: "black",
          borderWidth: "0",
          borderStyle: "dotted",
        });
      }
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
  display: grid;
  border: 4px solid black;
  gap: 3px;
  height: 400px;
  width: 400px;
  margin: 1rem;
  justify-content: space-between;
  align-items: space-between;
  // background-color: black;
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
  // border-width: 1px;
  width: 100%;
  height: 100%;
}
.grids-utils {
  padding: 1rem;
}

p {
  margin: 0.5rem 0;
}
</style>
