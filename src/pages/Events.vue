<template>
  <div class="Event">
    <Header/>
    <EventContent :dataItems="items" :dataFilter="{cities, regions, countries, problems}"/>
    <Pagination :current="currentPage()" :totalItems="totalITem" :perPage="perPage" @page-changed="changePage"/>
    <Footer/>
  </div>
</template>
<script>
import Header from '@/layout/header'
import EventContent from '@/layout/events'
import Pagination from '@/components/specialComponents/Paginate'
import Footer from '@/layout/footer'
import axios from 'axios'
const baseURL = 'http://localhost:3000/items'
export default {
  name: 'Event',
  components: {
    Header,
    EventContent,
    Pagination,
    Footer
  },
  data () {
    return {
      // totalItem: null,
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
  computed: {
    totalITem () {
      const totalItem = this.items.length
      return totalItem
    }
  },
  async created () {
    try {
      const items = await axios.get(baseURL)
      this.items = items.data
    } catch (e) {
      this.errors.push(e)
    }
  }
}
</script>
<style lang="scss">
.Event {
  background-color: $dark;
}
</style>
