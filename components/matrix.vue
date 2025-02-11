<template>
  <div class="matrix-container">
    <div class="y-axis font-mono">{{ matrixLabelX }}</div>

    <div class="matrix-cell-container">
      <div
        v-for="(row, rowIndex) in rows"
        :key="'row-' + rowIndex"
        class="matrix-row"
      >
        <div
          v-for="(cell, colIndex) in row"
          :key="'col-' + colIndex"
          class="matrix-cell"
          :style="{ backgroundColor: cell.color }"
        >
          <!-- Display the description for each cell -->
          <span>{{ cell.description }}</span>
        </div>
      </div>

      <div class="x-axis font-mono">{{ matrixLabelY }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MatrixComponent",
  props: {
    // Accept an array of objects where each object contains `description` and `color`
    matrixData: {
      type: Array,
      required: true,
    },
    matrixLabelX: {
      type: String,
      required: true,
    },
    matrixLabelY: {
      type: String,
      required: true,
    },
  },
  computed: {
    // Transform the flat matrixData array into rows
    rows() {
      const rowCount = Math.sqrt(this.matrixData.length); // Assuming the matrix is square
      const result = [];

      for (let i = 0; i < rowCount; i++) {
        result.push(this.matrixData.slice(i * rowCount, (i + 1) * rowCount));
      }

      return result;
    },
  },
};
</script>

<style scoped>
.x-axis {
  padding: 10px;
  border-top: 3px solid #93c5fd;
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.y-axis {
  writing-mode: sideways-lr;
  text-orientation: mixed;
  padding: 0 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.axis-label {
  margin: 0 10px;
}

.matrix-cell-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.matrix-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.matrix-row {
  display: flex;
  border-left: 3px solid #93c5fd;
}

.matrix-cell {
  width: 318px;
  height: 180px;
  border: 1px solid #000;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-size: 16px;
  margin: 5px;
  color: #fff; /* Text color to contrast with background */
}

.matrix-cell span {
  font-weight: bold;
}
</style>
