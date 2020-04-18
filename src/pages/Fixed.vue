<template>
  <div class="Fixed">
    <Header/>
    <FixedContent :dataItems="items" :dataFilter="{cities, regions, countries}"/>
    <Pagination :current="currentPage()" :totalItems="totalItem" :perPage="perPage" @page-changed="changePage"/>
    <Footer/>
  </div>
</template>
<script>
import Header from '@/layout/header'
import FixedContent from '@/layout/fixed'
import Pagination from '@/components/specialComponents/Pagination'
import Footer from '@/layout/footer'
import axios from 'axios'
const baseURL = 'http://localhost:3000/items'
const baseURL2 = 'http://localhost:3000/countries'
const baseURL3 = 'http://localhost:3000/regions'
const baseURL4 = 'http://localhost:3000/cities'
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
      countries: [],
      regions: [],
      cities: []
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
      const [items, countries, regions, cities] = await axios.all([
        axios.get(baseURL),
        axios.get(baseURL2),
        axios.get(baseURL3),
        axios.get(baseURL4)
      ])
      this.items = items.data
      this.countries = countries.data
      this.regions = regions.data
      this.cities = cities.data
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
