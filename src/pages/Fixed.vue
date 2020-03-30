<template>
  <div class="fixed">
    <Header :style="{ background: light }"/>
    <Fixed/>
    <Footer/>
  </div>
</template>

<script>
import Header from '@/layout/header'
import Footer from '@/layout/footer'
import Fixed from '@/layout/fixed'
export default {
  name: 'FFixed',
  components: {
    Header,
    Footer,
    Fixed
  },
  data () {
    return {
      light: '#201F30'
    }
  }
}
</script>
<style lang="scss">
</style>
