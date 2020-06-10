<template>
  <div class="table">
    <div
      class="group"
      v-for="(group, groupIndex) in shipmentData"
      :key="groupIndex"
    >
      <div class="table-row" v-for="(row, rowIndex) in group" :key="rowIndex">
        <div
          :class="['table-column']"
          v-for="(cell, colIndex) in row"
          :key="colIndex"
        >
          <span v-show="rowIndex === 0 || (colIndex !== 0 && colIndex !== 1)">{{
            cell.value
          }}</span>
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
      checkedStates: [
        [false, false, false],
        [false, false]
      ],
      shipmentFields: [
        { value: "", width: "3.2%", selected: true },
        { value: "출하일자", width: "5.8%" },
        { value: "주문번호", width: "6.5%" },
        { value: "납품처", width: "7.1%" },
        { value: "납품주소", width: "10.4%" },
        { value: "품명 규격", width: "15.9%" },
        { value: "색상", width: "4.5%" },
        { value: "조장", width: "4.5%" },
        { value: "조장수", width: "4.5%" },
        { value: "수량", width: "4.5%" },
        { value: "배차여부", width: "4.7%" },
        { value: "기사이름", width: "6.1%" },
        { value: "전화번호", width: "7.1%" },
        { value: "차량번호", width: "6.1%" },
        { value: "차종", width: "4.5%" },
        { value: "톤수", width: "4.6%" }
      ],
      shipmentData: [
        [
          [
            { value: "", width: "3.2%", selected: true },
            { value: "2020-06-03", width: "5.8%" },
            { value: "5888888888", width: "6.5%" },
            { value: "범일케이블", width: "7.1%" },
            {
              value: "경기 하남시 덕풍동",
              width: "10.4%"
            },
            {
              value: "450 / 750V HFIX + (SE.) 2.5SQ(1/78)",
              width: "15.9%"
            },
            { value: "RD", width: "4.5%" },
            { value: "100", width: "4.5%" },
            { value: 300, width: "4.5%" },
            { value: 3000, width: "4.5%" },
            { value: "N", width: "4.7%" },
            { value: "", width: "6.1%" },
            { value: "", width: "7.1%" },
            { value: "", width: "6.1%" },
            { value: "", width: "4.5%" },
            { value: "", width: "4.6%" }
          ],
          [
            { value: "", width: "3.2%", selected: true },
            { value: "2020-06-03", width: "5.8%" },
            { value: "5888888888", width: "6.5%" },
            { value: "범일케이블", width: "7.1%" },
            {
              value: "경기 하남시 덕풍동",
              width: "10.4%"
            },
            {
              value: "450 / 750V HFIX + (SE.) 2.5SQ(1/78)",
              width: "15.9%"
            },
            { value: "RD", width: "4.5%" },
            { value: "100", width: "4.5%" },
            { value: 300, width: "4.5%" },
            { value: 3000, width: "4.5%" },
            { value: "Y", width: "4.7%" },
            { value: "김필주", width: "6.1%" },
            { value: "010-3249-4546", width: "7.1%" },
            { value: "인천마2840", width: "6.1%" },
            { value: "윙카", width: "4.5%" },
            { value: "1", width: "4.6%" }
          ],
          [
            { value: "", width: "3.2%", selected: true },
            { value: "2020-06-03", width: "5.8%" },
            { value: "5888888888", width: "6.5%" },
            { value: "범일케이블", width: "7.1%" },
            {
              value: "경기 하남시 덕풍동",
              width: "10.4%"
            },
            {
              value: "450 / 750V HFIX + (SE.) 2.5SQ(1/78)",
              width: "15.9%"
            },
            { value: "RD", width: "4.5%" },
            { value: "100", width: "4.5%" },
            { value: 300, width: "4.5%" },
            { value: 3000, width: "4.5%" },
            { value: "Y", width: "4.7%" },
            { value: "김필주", width: "6.1%" },
            { value: "010-3249-4546", width: "7.1%" },
            { value: "인천마2840", width: "6.1%" },
            { value: "윙카", width: "4.5%" },
            { value: "1", width: "4.6%" }
          ]
        ],
        [
          [
            { value: "", width: "3.2%", selected: true },
            { value: "2020-06-03", width: "5.8%" },
            { value: "5261237678", width: "6.5%" },
            { value: "송송케이블", width: "7.1%" },
            {
              value: "경기 하남시 덕풍동",
              width: "10.4%",
              row: 1,
              groupSize: 2
            },
            {
              value: "450 / 750V HFIX + (SE.) 2.5SQ(1/78)",
              width: "15.9%",
              row: 1,
              groupSize: 2
            },
            { value: "RD", width: "4.5%" },
            { value: "100", width: "4.5%" },
            { value: 300, width: "4.5%" },
            { value: 3000, width: "4.5%" },
            { value: "N", width: "4.7%" },
            { value: "", width: "6.1%" },
            { value: "", width: "7.1%" },
            { value: "", width: "6.1%" },
            { value: "", width: "4.5%" },
            { value: "", width: "4.6%" }
          ],
          [
            { value: "", width: "3.2%", selected: true },
            { value: "2020-06-03", width: "5.8%" },
            { value: "5261237678", width: "6.5%" },
            { value: "송송케이블", width: "7.1%" },
            {
              value: "경기 하남시 덕풍동",
              width: "10.4%"
            },
            {
              value: "450 / 750V HFIX + (SE.) 2.5SQ(1/78)",
              width: "15.9%"
            },
            { value: "RD", width: "4.5%" },
            { value: "100", width: "4.5%" },
            { value: 300, width: "4.5%" },
            { value: 3000, width: "4.5%" },
            { value: "N", width: "4.7%" },
            { value: "", width: "6.1%" },
            { value: "", width: "7.1%" },
            { value: "", width: "6.1%" },
            { value: "", width: "4.5%" },
            { value: "", width: "4.6%" }
          ]
        ]
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
