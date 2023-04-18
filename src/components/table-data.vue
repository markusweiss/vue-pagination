<template>
  <div ref="tabledata">
    <h1>{{ headline }}</h1>
    <table>
      <thead>
        <tr>
          <th>id #</th>
          <th>Name</th>
          <th>City</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in itemList" :key="index">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.city }}</td>
        </tr>        
        <tr v-if="this.items.length > showPerPage"> 
          <td colspan="3">
                <pagination @pageNumber="handlePages" :number-of-entries=numberOfEntries :pages-display-single="true" :pages-display-from-to="false" :show-per-page=showPerPage prev-text="zurück" next-text="weiter"></pagination>
          </td>
        </tr>  
      </tbody>
    </table>
  </div>
</template>

<script>
import Pagination from './pagination.vue'

export default {
  name: "TableData",
   components: {
    Pagination
  },
  props: {
    headline: {
      type: [String],
      default: "",
    },
    items: {
      type: [Array],
      default: () => [],
    },
  },
  data() {
    return {
      currentPage: 1,
      showPerPage: 5,
      disableNext: false,
      disablePrev: true,
    };
  },
  computed: {
    numberOfEntries() {
      return Math.ceil(this.items.length);
    },
    
    numberOfPages() {
      return Math.ceil(this.items.length / this.showPerPage);
    }, 
    indexStart() {
      return (this.currentPage - 1) * this.showPerPage;
    },
    indexEnd() {
      return this.indexStart + this.showPerPage;
    }, 
    itemList() {
      return this.items.slice(this.indexStart, this.indexEnd);
    },
  },
  methods: {
    handlePages(index) {
      if (!(this.currentPage === index)) {
        this.currentPage = index;
      }
    },
  },
};
</script>
