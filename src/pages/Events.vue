<template>
  <div class="Event">
    <Header/>
    <EventContent :dataItems="items"/>
    <Footer/>
  </div>
</template>

<script>
import Header from '@/layout/header'
import EventContent from '@/layout/events'
import Footer from '@/layout/footer'
import axios from 'axios'
const baseURL = 'http://localhost:3000/items'
export default {
  name: 'Event',
  components: {
    Header,
    EventContent,
    Footer
  },
  data () {
    return {
      dark: '#1B1919',
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
}
</script>
<style lang="scss">
.Event {
  background-color: $dark;
}
</style>
