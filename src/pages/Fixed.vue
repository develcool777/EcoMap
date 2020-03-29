<template>
  <div class="fixed">
    <Header/>
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
  }
}
</script>
<style lang="scss">
</style>
