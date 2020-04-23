<template>
  <header class="header">
    <div class="wrapper">
      <div class="header__flex">
        <HeaderLogo/>
        <HeaderMenu/>
        <HeaderAccLanSer :languages="languages"/>
      </div>
    </div>
  </header>
</template>

<script>
import HeaderLogo from '@/components/headerComponents/headerLogo'
import HeaderMenu from '@/components/headerComponents/headerMenu'
import HeaderAccLanSer from '@/components/headerComponents/headerAccLanSer'
export default {
  name: 'Header',
  components: {
    HeaderLogo,
    HeaderMenu,
    HeaderAccLanSer
  },
  data () {
    return {
      languages: [
        { id: 1, name: 'EN' },
        { id: 2, name: 'RU' },
        { id: 3, name: 'UA' }
      ]
    }
  }
}
</script>
<style lang="scss">
.header {
  padding: rem(10) 0;
  &__flex {
    @include FCenter(space-between);
  }
}
</style>
