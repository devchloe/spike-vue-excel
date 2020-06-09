<template>
  <div id="app">
    <!--        <excel-uploader/>-->
    <sample-table />
    <sample-table-using-table />
  </div>
</template>

<script>
// import ExcelUploader from "./components/ExcelUploader";

import SampleTable from "./components/SampleTable";
import SampleTableUsingTable from "./components/SampleTableUsingTableCell";
export default {
  name: "App",
  components: {
    SampleTableUsingTable,
    SampleTable
    // ExcelUploader,
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
