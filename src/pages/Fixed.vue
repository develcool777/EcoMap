<template>
  <div class="fixed">
    <Header/>
    <FixedContent :dataItems="items"/>
    <Pagination :current="currentPage" :total="totalItem" :per-page="perPage" @page-changed="items"/>
    <Footer/>
  </div>
</template>

<script>
import Header from '@/layout/header'
import FixedContent from '@/layout/fixed'
import Pagination from '@/components/specialComponents/pagination'
import Footer from '@/layout/footer'
import axios from 'axios'
const baseURL = 'http://localhost:7000/items'
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
      light: '#201F30',
      photos: [],
      totalItem: 16,
      perPage: 3,
      currentPage: 1,
      items: []
    }
  },
  async created () {
    try {
      const res = await axios.get(baseURL)
      this.items = res.data
      console.log(res.data)
      console.log(res.status)
      console.log(res.statusText)
      console.log(res.headers)
      console.log(res.config)
    } catch (e) {
      console.error(e)
    }
  }
  // methods: {
  //   fetchPhotos: function(page) {
  //     // var options = {
  //       // params: {
  //         // client_id: appId,
  //       //   page: page,
  //       //   per_page: this.perPage
  //       // }
  //     // }

  //     this.$http.get('https://api.unsplash.com/photos', options).then(function(response) {

  //       this.photos = response.data

  //       this.totalPhotos = parseInt(response.headers.get('x-total'))

  //       this.currentPage = page

  //     }, console.log)
  //   }
  // },
  // created () {
  //   this.fetchPhotos(this.currentPage)
  // }
}
</script>
<style lang="scss">
.fixed {
  background-color: $backgroundColor;
}
</style>
