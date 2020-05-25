<template>
  <div class="Fixed">
    <Header/>
    <FixedContent :dataItems="items" :dataFilter="{cities, regions, countries, problems}"/>
    <Pagination :current="currentPage()" :totalItems="totalItem" :perPage="perPage" @page-changed="changePage"/>
    <Footer/>
  </div>
</template>
<script>
import Header from '@/layout/header'
import FixedContent from '@/layout/fixed'
import Pagination from '@/components/specialComponents/Paginate'
import Footer from '@/layout/footer'
import axios from 'axios'
const baseURL = 'http://localhost:3000/items'
export default {
  name: 'Fixed',
  components: {
    Header,
    Footer,
    FixedContent,
    Pagination
  },
  data () {
    return {
      totalItem: 8,
      perPage: 3,
      current: 1,
      items: [],
      countries: [
        { id: 1, name: 'Ukraine' },
        { id: 2, name: 'Spain' }
      ],
      regions: [
        { id: 1, name: 'Kievska' },
        { id: 2, name: 'New York' }
      ],
      cities: [
        { id: 1, name: 'Kiev' },
        { id: 2, name: 'Chernivtsi' }
      ],
      problems: [
        { id: 1, name: 'first' },
        { id: 2, name: 'second' }
      ]
    }
  },
  methods: {
    currentPage () {
      return this.current
    },
    async changePage (page) {
      this.current = page
    }
  },
  async created () {
    try {
      const items = await axios.get(baseURL)
      axios.get(baseURL)
      this.items = items.data
    } catch (e) {
      this.errors.push(e)
    }
  }
}
</script>
<style lang="scss">
.Fixed {
  background-color: $backgroundColor;
}
</style>
