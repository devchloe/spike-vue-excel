<template>
  <div>
    <label>
      File
      <input type="file" accept=".xlsx, .xls" @input="handleFile" />
    </label>
    <button @click="exportToExcel">Export</button>
    <table v-for="(data, index) in excelDataList" :key="index">
      <thead>
        <tr>
          <th v-for="(item, index) in data.header" :key="index">
            {{ item }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, index) in data.results" :key="index">
          <td v-for="(cell, index) in row" :key="index" contenteditable="true">
            {{ cell }}
          </td>
        </tr>
      </tbody>
    </table>
    <table id="sheetjs">
      <tr>
        <td>S</td>
        <td>h</td>
        <td>e</td>
        <td>e</td>
        <td>t</td>
        <td>J</td>
        <td>S</td>
      </tr>
      <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
      </tr>
      <tr>
        <td>2</td>
        <td>3</td>
        <td>4</td>
        <td>5</td>
        <td>6</td>
        <td>7</td>
        <td>8</td>
      </tr>
    </table>

      <button @click="exportSelected">선택한 로우 export</button>
    <div class="row">
      <div class="col-xs-12">
        <div class="table-responsive">
          <table class="table table-striped">
            <thead>
              <tr>
                <th>Select</th>
                <th v-for="c in cols" :key="c.key">{{ c.name }}</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(r, key) in data" :key="key">
                  <input value="true" name="product" type="checkbox" v-model="checkBox" />
                  <td v-for="c in cols" :key="c.key">{{ r[c.key] }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import XLSX from "xlsx";

const make_cols = refstr =>
  Array(XLSX.utils.decode_range(refstr).e.c + 1)
    .fill(0)
    .map((x, i) => ({ name: XLSX.utils.encode_col(i), key: i }));

export default {
  name: "ExcelUploader",
  data() {
    return {
      excelDataList: [
        {
          header: null,
          results: null
        }
      ],
      checkBox: [],
      data: ["SheetJS".split(""), "1234567".split("")],
      cols: [
        { name: "A", key: 0 },
        { name: "B", key: 1 },
        { name: "C", key: 2 },
        { name: "D", key: 3 },
        { name: "E", key: 4 },
        { name: "F", key: 5 },
        { name: "G", key: 6 }
      ]
    };
  },
  methods: {
    drawData(list) {
      this.excelDataList = list;
    },
    handleFile(e) {
      const files = e.target.files;

      if (files.length !== 1) {
        console.log("possible to select only one file");
        return;
      }

      const targetFile = files[0];
      // this.readFile(targetFile);
      this._file(targetFile);
    },
    readFile(file) {
      const reader = new FileReader();
      // TODO readerAsArrayBuffer 메서드가 실행되고 파일이 load 되었을 때 실행되는 이벤트 리스
      reader.onload = e => {
        let list = [];
        const data = e.target.result;
        const workbook = XLSX.read(data, { type: "array" });

        // const firstSheetName = workbook.SheetNames[0];
        // console.log(workbook.SheetNames);
        for (let sheetName of workbook.SheetNames) {
          const worksheet = workbook.Sheets[sheetName];
          const header = this.getHeaderRow(worksheet);

          // console.log('merges: ', worksheet['!merges']);
          // console.log(this.getSpecificColumn(worksheet, 'B'));
          // console.log('cols: ', XLSX.utils.decode_cell('B2'));
          // console.log(XLSX.utils.decode_col('C'));

          const results = XLSX.utils.sheet_to_json(worksheet);
          // console.log("header: ", header);
          // console.log("results: ", results);

          list.push({ header, results });
        }
        this.drawData(list);
      };

      reader.readAsArrayBuffer(file);
    },
    getHeaderRow(sheet) {
      const headers = [];
      const range = XLSX.utils.decode_range(sheet["!ref"]);
      // console.log(range);
      let C;
      const R = range.s.r;
      /* start in the first row */
      for (C = range.s.c; C <= range.e.c; ++C) {
        /* walk every column in the range */
        const cell = sheet[XLSX.utils.encode_cell({ c: C, r: R })]; // cell 주소값
        /* find the cell in the first row */
        let hdr = "UNKNOWN " + C; // <-- replace with your desired default
        if (cell && cell.t) hdr = XLSX.utils.format_cell(cell); // cell의 값을 text로 생성
        headers.push(hdr);
      }
      return headers;
    },
    getSpecificColumn(sheet) {
      const columns = [];
      const range = XLSX.utils.decode_range(sheet["!ref"]);

      let R;
      for (R = range.s.r; R <= range.e.r; ++R) {
        const cell = sheet[XLSX.utils.encode_cell({ c: range.s.c, r: R })];
        let col = "";
        if (cell && cell.t) col = XLSX.utils.format_cell(cell);
        columns.push(col);
      }
      return columns;
    },
    exportToExcel() {
      var sheet1 = XLSX.utils.json_to_sheet(this.excelDataList[0].results);
      var sheet2 = XLSX.utils.json_to_sheet(this.excelDataList[1].results);

      // A workbook is the name given to an Excel file
      var wb = XLSX.utils.book_new(); // make Workbook of Excel

      // add Worksheet to Workbook
      // Workbook contains one or more worksheets
      XLSX.utils.book_append_sheet(wb, sheet1, "sheet1"); // sheetAName is name of Worksheet
      XLSX.utils.book_append_sheet(wb, sheet2, "sheet2"); // sheetAName is name of Worksheet

      var tbl = document.getElementById("sheetjs");
      var tableToBook = XLSX.utils.table_to_book(tbl, { type: "string" });

      // export Excel file
      XLSX.writeFile(wb, "sample.xlsx"); // name of the file is 'book.xlsx'
      XLSX.writeFile(tableToBook, "tableToBook.xlsx"); // name of the file is 'book.xlsx'
    },
    exportSelected() {
      let json = [];
      this.checkBox.forEach((check, i) => {
        if (check) {
          json.push(this.data[i]);
        }
      });
        const sheet = XLSX.utils.json_to_sheet(json);
        const wb = XLSX.utils.book_new();

        XLSX.utils.book_append_sheet(wb, sheet, "sheet1");

        XLSX.writeFile(wb, "sample2.xlsx");
    },
    _file(file) {
      /* Boilerplate to set up FileReader */
      const reader = new FileReader();
      reader.onload = e => {
        /* Parse data */
        const bstr = e.target.result;
        const wb = XLSX.read(bstr, { type: "binary" });
        /* Get first worksheet */
        const wsname = wb.SheetNames[0];
        const ws = wb.Sheets[wsname];
        /* Convert array of arrays */
        const data = XLSX.utils.sheet_to_json(ws, { header: 1 });
        /* Update state */
        this.data = data.map(row => ({...row, selected: true}));
        this.cols = make_cols(ws["!ref"]);
      };
      reader.readAsBinaryString(file);
    }
  }
};
</script>

<style scoped>
table,
th,
tr,
td {
  border: 1px solid black;
}
</style>
