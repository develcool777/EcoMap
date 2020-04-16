<template>
  <div class="Event">
    <Header/>
    <EventContent :dataItems="items" :datas="dataForFilter"/>
    <Pagination :current="currentPage()" :totalItems="totalItem" :perPage="perPage" @page-changed="changePage"/>
    <Footer/>
  </div>
</template>

<script>
import Header from '@/layout/header'
import EventContent from '@/layout/events'
import Pagination from '@/components/specialComponents/Pagination'
import Footer from '@/layout/footer'
import axios from 'axios'
const baseURL = 'http://localhost:3000/items'
const baseURL2 = 'http://localhost:3000/dataForFilter'
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
      totalItem: 8,
      perPage: 3,
      current: 1,
      items: [],
      dataForFilter: []
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
  created () {
    axios.all([
      axios.get(baseURL),
      axios.get(baseURL2)
    ])
      .then((responses) => {
        const temp1 = responses[0]
        const temp2 = responses[1]
        this.items = temp1.data
        this.dataForFilter = temp2.data
      })
      .catch(e => {
        this.errors.push(e)
      })
  }
}
</script>
<style lang="scss">
.Event {
  background-color: $dark;
}
</style>
