<template>
  <ul class="pagination">
    <li
      id="first"
      :class="['pagination__page-item', { disabled: isFirstPage }]"
      @click.stop="goToFirst"
    >
      <span class="page-link page-first"></span>
    </li>
    <li
      id="prev"
      :class="['pagination__page-item', { disabled: isFirstPage }]"
      @click.stop="goToPrev"
    >
      <span class="page-link page-prev"></span>
    </li>
    <li
      :class="[
        'pagination__page-item',
        'page-number',
        { active: currentPage === pageNumber }
      ]"
      v-for="(pageNumber, index) in selectablePages"
      :key="index"
      @click.stop="onClick(pageNumber)"
    >
      <a class="page-link">{{ pageNumber }}</a>
    </li>
    <li
      id="next"
      :class="['pagination__page-item', { disabled: isLastPage }]"
      @click.stop="goToNext"
    >
      <span class="page-link page-next"></span>
    </li>
    <li
      id="last"
      :class="['pagination__page-item', { disabled: isLastPage }]"
      @click.stop="goToLast"
    >
      <span class="page-link page-last"></span>
    </li>
  </ul>
</template>

<script>
const DEFAULT_PER_PAGE = 10;
const DEFAULT_TOTAL_ROWS = 0;
const DEFAULT_UNIT_PAGE_SIZE = 10;

const sanitizePerPage = value => {
  const perPage = parseInt(value, 10) || DEFAULT_PER_PAGE;
  return perPage < 1 ? 1 : perPage;
};
const sanitizeTotalRows = value => {
  const totalRows = parseInt(value, 10) || DEFAULT_TOTAL_ROWS;
  return totalRows < 0 ? 0 : totalRows;
};
export default {
  name: "AppPagination",
  model: {
    prop: "value",
    event: "change"
  },
  props: {
    value: {
      type: [String, Number],
      default: 1
    },
    totalRows: {
      type: [String, Number],
      default: DEFAULT_TOTAL_ROWS
    },
    perPage: {
      type: [String, Number],
      default: DEFAULT_PER_PAGE
    },
    unitPageSize: {
      type: [String, Number],
      default: DEFAULT_UNIT_PAGE_SIZE
    }
  },
  data() {
    return {
      currentPage: 0
    };
  },
  computed: {
    numberOfPages() {
      const result = Math.ceil(
        sanitizeTotalRows(this.totalRows) / sanitizePerPage(this.perPage)
      );

      return result < 1 ? 1 : result;
    },
    selectablePages() {
      let centerOfUnitPageSize = Math.floor(this.unitPageSize / 2);
      let result = [];

      if (this.numberOfPages <= this.unitPageSize) {
        for (let i = 1; i <= this.numberOfPages; i++) {
          result.push(i);
        }
      } else {
        if (this.currentPage <= centerOfUnitPageSize) {
          for (let i = 1; i <= this.unitPageSize; i++) {
            result.push(i);
          }
        } else if (
          this.currentPage >
          this.numberOfPages - (centerOfUnitPageSize - 1)
        ) {
          for (
            let i = this.numberOfPages - (this.unitPageSize - 1);
            i <= this.numberOfPages;
            i++
          ) {
            result.push(i);
          }
        } else {
          for (
            let i = this.currentPage - centerOfUnitPageSize;
            i <= this.currentPage + (centerOfUnitPageSize - 1);
            i++
          ) {
            result.push(i);
          }
        }
      }
      return result;
    },
    isFirstPage() {
      return this.currentPage === 1;
    },
    isLastPage() {
      return this.currentPage === this.numberOfPages;
    }
  },
  watch: {
    totalRows: function() {
      this.currentPage = 1;
      this.$emit("change", this.currentPage);
    }
  },
  created() {
    const currentPage = parseInt(this.value, 10) || 0;

    if (currentPage > 0) {
      this.currentPage = currentPage;
    } else {
      this.$nextTick(() => {
        this.currentPage = 0;
      });
    }
  },
  methods: {
    onClick(num) {
      this.currentPage = num;
      this.$emit("change", this.currentPage);
    },
    goToFirst() {
      this.currentPage = 1;
      this.$emit("change", this.currentPage);
    },
    goToPrev() {
      if (this.isFirstPage) return;

      this.currentPage = this.currentPage - 1;
      this.$emit("change", this.currentPage);
    },
    goToNext() {
      if (this.isLastPage) return;

      this.currentPage = this.currentPage + 1;
      this.$emit("change", this.currentPage);
    },
    goToLast() {
      this.currentPage = this.numberOfPages;
      this.$emit("change", this.currentPage);
    }
  }
};
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: space-around;
  align-items: center;
  cursor: pointer;
  list-style: none;

  .__page-item {
    padding: 0.5rem 0.75rem;

    > .page-first,
    .page-prev,
    .page-next,
    .page-last {
      opacity: 0.6;
    }

    &.active {
      color: dodgerblue;
      font-weight: bold;
    }

    &.disabled {
      color: grey;
      cursor: default !important;
    }
  }
}
</style>
