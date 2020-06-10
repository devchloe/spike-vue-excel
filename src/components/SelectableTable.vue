<template>
  <div id="app">
    <div @click="$emit('all-clicked')">Click All!</div>
    <div v-for="(group, index) in data" :key="index">
      <div
        :class="['row', { 'row-selected': selected2.some(x => x === row.id) }]"
        v-for="(row, index) in group.rows"
        :key="index"
      >
        <div class="cell checkbox">
          <!--          <input type="checkbox" :value="row.id" v-model="selected" />-->
          <div @click="click(row.id)">check {{ row.id }}>></div>
        </div>
        <div class="cell" style="width: 20%">{{ row.id }}</div>
        <div class="cell" style="width: 40%">{{ row.name }}</div>
        <div class="cell" style="width: 40%">{{ row.email }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SelectableTable",
  props: {
    selected2: Array,
    data: Array
  },
  data() {
    return {
      groups: [
        {
          label: "school1",
          rows: [
            {
              id: "id1",
              name: "John Doe",
              email: "email@example.com"
            },
            {
              id: "id2",
              name: "Jone Doe",
              email: "email2@example.com"
            }
          ]
        },
        {
          label: "school2",
          rows: [
            {
              id: "id3",
              name: "John Doe2",
              email: "email@example.com"
            },
            {
              id: "id4",
              name: "Jone Doe2",
              email: "email2@example.com"
            }
          ]
        }
      ]
    };
  },
  methods: {
    click(id) {
      this.$emit("click-check", id);
    },

    select2() {
      this.selected2 = [];
      if (!this.selected2) {
        for (let i in this.groups.rows) {
          this.selected2.push(this.group.map(g => g.rows[i].id));
        }
      }
    }
  }
};
</script>

<style scoped>
.row {
  display: flex;
}
.row:last-child {
  border-bottom: 1px solid black;
}

input[type="checkbox"] {
  display: none;
}

input[type="checkbox"] {
  display: inline-block;
  vertical-align: middle;
  width: 45px;
  height: 45px;
  background: url(../assets/uncheck.png) 0px center no-repeat;
}
input[type="checkbox"]:checked {
  background: url(../assets/check.png) -48px center no-repeat;
}
label {
  cursor: pointer;
  color: #555;
}

.row-selected {
  background-color: #ffcef2;
}
.checked {
  background-color: yellowgreen;
}
</style>

/** https://vuejsexamples.com/vuejs-tables-and-select-all-checkbox/ 샘플
https://codepen.io/nikitamarcius/pen/LQOaxd?editors=0010
https://codepen.io/rolchau/pen/rlAtq/ */
