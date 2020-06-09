<template>
  <div class="table">
    <div class="group" v-for="(group, index) in groups" :key="index">
      <div class="table-row" v-for="(row, rowIndex) in group" :key="rowIndex">
        <div
          :class="['table-column']"
          v-for="(cell, colIndex) in row"
          :key="colIndex"
        >
            <span v-show="rowIndex === 0 || (colIndex !== 0 && colIndex !== 1)">{{ cell.value }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SampleTable",
  data() {
    return {
      groups: [
        [
          [{ value: "AAAAAAA1" }, { value: "AAAAAAA2" }, { value: "BBBBBBB1" }],
          [{ value: "AAAAAAA1" }, { value: "AAAAAAA2" }, { value: "BBBBBBB2" }],
          [{ value: "AAAAAAA1" }, { value: "AAAAAAA2" }, { value: "BBBBBBB3" }],
          [{ value: "AAAAAAA1" }, { value: "AAAAAAA2" }, { value: "BBBBBBB4" }]
        ],
        [
          [{ value: "AAAAAAA1" }, { value: "AAAAAAA2" }, { value: "CCCCCCC1" }],
          [{ value: "AAAAAAA1" }, { value: "AAAAAAA2" }, { value: "CCCCCCC2" }]
        ],
        [[{ value: "AAAAAAA1" }, { value: "AAAAAAA2" }, { value: "DDDDD1" }]]
      ]
    };
  }
};
</script>

<style scoped>
.table-row {
  display: flex;
}
.table-row:last-child {
  border-bottom: 1px solid black;
}
.table-column {
  width: 20%;
}
.table-column-value-hidden {
  visibility: hidden;
}
</style>
