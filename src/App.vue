<template>
  <div class="container">
  <table-data headline="Tabelle mit Mockdaten" :items=items></table-data>

  <h2>Komponente mit Zahlen</h2>
  <pagination @pageNumber="handlePages" :number-of-entries=numberOfEntries :pages-display-single="true" :pages-display-from-to="false" :show-per-page=showPerPage prev-text="prev" next-text="next"></pagination>
  
  <h2>Komponente mit x/y</h2>
  <pagination @pageNumber="handlePages" :number-of-entries=numberOfEntries :pages-display-single="false" :pages-display-from-to="true" :show-per-page=showPerPage prev-text="prev" next-text="next"></pagination>
  </div>
</template>

<script>

import('./style.css')
import TableData from './components/table-data.vue'
import Pagination from './components/pagination.vue'
import itemsData from './mock.json'

export default {
  name: 'App',
  components: {
    Pagination, TableData
  },
  data() {
    return {
      items: itemsData
    }
  }
}
</script>
