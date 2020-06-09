<template>
  <div class="table">
    <div class="row rowspan">
      <div class="cell">cell 1</div>
      <div class="cell">cell 2</div>
    </div>
    <div class="row">
      <div class="cell colspan">
        <div>
          <div>
            cell 3
          </div>
        </div>
      </div>
      <div class="cell"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SampleTableUsingTable"
};
</script>

<style scoped>
div.table {
  display: table;
  width: 100px;
  background-color: lightblue;
  border-collapse: collapse;
  border: 1px solid red;
}

div.row {
  display: table-row;
}

div.cell {
  display: table-cell;
  border: 1px solid red;
}

div.colspan,
div.colspan + div.cell {
  border: 0;
}

div.rowspan + div.row {
  border: 0;
}
div.colspan > div {
  width: 1px;
}

div.colspan > div > div {
  position: relative;
  width: 99px;
  overflow: hidden;
}
</style>
