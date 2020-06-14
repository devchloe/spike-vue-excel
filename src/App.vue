<template>
  <div id="app">
    <div v-for="(product, index) in showProducts" :key="index">
      {{ product }}
    </div>
    {{ currentPage }} , {{ perPage }}
    <app-pagination
      v-model="currentPage"
      :total-rows="products.length"
      :per-page="perPage"
      @change="changePage"
    />
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
import AppPagination from "./components/AppPagination";
export default {
  name: "App",
  components: { AppPagination, SelectableTable },
  data() {
    return {
      products: ["product1", "product2", "product3", "product4", "product5"],
      currentPage: 1,
      perPage: 2,
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
  computed: {
    showProducts() {
      return this.products.slice(
        this.currentPage * this.perPage - this.perPage,
        this.currentPage * this.perPage
      );
    }
  },
  methods: {
    changePage(page) {
      this.currentPage = page;
      console.log("page-changed");
    },
    onClickCheck(id) {
      console.log(id);
      if (this.selected.some(x => x === id)) {
        this.selected = this.selected.filter(x => x !== id);
      } else {
        this.selected.push(id);
      }
    },
    onSelectAll() {
      if (
        this.selected.length ===
        this.groups.map(({ rows }) => rows).flat().length
      ) {
        this.selected = [];
      } else {
        this.selected = this.groups
          .map(({ rows }) => rows)
          .flat()
          .map(({ id }) => id);
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
