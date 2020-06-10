<template>
  <div id="app">
    <selectable-table
      :data="groups"
      :selected2="selected"
      @click-check="onClickCheck"
      @all-clicked="onSelectAll"
    />
    COUNT:: {{ selected.length }}
  </div>
</template>

<script>
import SelectableTable from "./components/SelectableTable";
export default {
  name: "App",
  components: { SelectableTable },
  data() {
    return {
      result: 0,
      selected: [],
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
    onClickCheck(id) {
      console.log(id);
      if (this.selected.some(x => x === id)) {
        this.selected = this.selected.filter(x => x !== id);
      } else {
        this.selected.push(id);
      }
    },
    onSelectAll() {
      if (this.selected.length === this.groups.map(({ rows }) => rows).flat().length) {
        this.selected = [];
      } else {
        this.selected = this.groups.map(({ rows }) => rows).flat().map(({ id }) => id);
      }
      // this.selected = [];
      // if (!this.selected) {
      //   for (let i in this.groups.rows) {
      //     this.selected.push(this.group.map(g => g.rows[i].id));
      //   }
      // }
    }
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
}
</style>
