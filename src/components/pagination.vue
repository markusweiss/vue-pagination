<template>
  <ul>
    <li class="prev">
      <a :class="{ disabled: disablePrev }" @click="prev()"> {{ prevText }} </a>
    </li>
    <slot v-if="pagesDisplaySingle">
      <li v-for="index in numberOfPages" :key="index" :value="index">
        <a v-if="currentPage === index" class="active">{{ index }}</a>
        <a v-else @click="selectPage(index)">{{ index }}</a>
      </li>
    </slot>
    <li v-if="pagesDisplayFromTo" class="pageNumber">
      {{ currentPage }} {{ fromText }} {{ numberOfPages }}
    </li>
    <li class="next">
      <a :class="{ disabled: disableNext }" @click="next()"> {{ nextText }} </a>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Pagination",
  props: {
    prevText: {
      type: [String],
      default: "prev",
    },
    nextText: {
      type: [String],
      default: "next",
    },
    fromText: {
      type: [String],
      default: " / ",
    },
    numberOfEntries: {
      type: [Number],
       default: 10,
    },
    showPerPage: {
      type: [Number],
      default: 3,
    },
    pagesDisplayFromTo: {
      type: [Boolean],
      default: false,
    },
    pagesDisplaySingle: {
      type: [Boolean],
      default: false,
    },
  },
  data() {
    return {
      currentPage: 1,
      disableNext: false,
      disablePrev: true,
    };
  },
  computed: {
    numberOfPages() {
      return Math.ceil(this.numberOfEntries / this.showPerPage);
    },
  },
  methods: {
    selectPage(index) {
      console.log("Index::", index);
      if (!(this.currentPage === index)) {
        this.currentPage = index;
        this.$emit('pageNumber', index);
      }
      if (this.currentPage >= 2) {
        this.disablePrev = false;
      } else {
        this.disablePrev = true;
      }
      if (this.currentPage >= this.numberOfPages) {
        this.disableNext = true;
      } else {
        this.disableNext = false;
      }
    },
    prev() {
      if (!(this.currentPage <= 1)) {
        this.disableNext = false;
        if (this.currentPage - 1 <= 1 || 0) {
          this.disablePrev = true;
        }
        this.$emit('pageNumber', this.currentPage-1);
        return this.currentPage--;
      }
    },
    next() {
      if (!(this.currentPage >= this.numberOfPages)) {
        this.disablePrev = false;
        if (this.currentPage + 1 >= this.numberOfPages) {
          this.disableNext = true;
        }
        this.$emit('pageNumber', this.currentPage+1);
        return this.currentPage++;
      }
    },
  },
};
</script>