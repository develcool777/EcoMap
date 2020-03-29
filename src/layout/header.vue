<template>
  <header class="header">
    <div class="wrapper">
      <div class="header__flex">
        <HeaderLogo/>
        <HeaderMenu/>
        <HeaderAccLanSer/>
      </div>
    </div>
  </header>
</template>

<script>
import HeaderLogo from '@/components/headerLogo'
import HeaderMenu from '@/components/headerMenu'
import HeaderAccLanSer from '@/components/headerAccLanSer'
export default {
  name: 'Header',
  components: {
    HeaderLogo,
    HeaderMenu,
    HeaderAccLanSer
  }
}
</script>
<style lang="scss">
.header {
  background-color: $backgroundColor;
  padding: rem(10) 0;
  &__flex {
    @include FCenter(space-between);
  }
}
</style>
