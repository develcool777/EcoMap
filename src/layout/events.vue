<template>
  <div class="contentEvent">
    <div class="wrapper">
      <div class="contentEvent__title">Events</div>
      <form class="contentEvent__filters">
        <div class="contentEvent__filterItem" v-for="i in 3" :key="i">
          <select name="" id="" class="contentEvent__select">
            <option v-for="(c, i) in computedObj" :key="i" :value="c" class="hals__option" >{{ c }}</option>
          </select>
        </div>
        <!-- <select name="" id="" class=contentEvent__select">
          <option v-for="(r, i) in regions" :key="i" :value="r" class="hals__option" >{{ r }}</option>
        </select>
        <select name="" id="" class=contentEvent__select">
          <option v-for="(c, i) in cites" :key="i" :value="c" class="hals__option" >{{ c }}</option>
        </select> -->
      </form>
      <div class="contentEvent__items">
        <Item v-for="item in dataItems"  :key="item.id" :fitem="item"/>
      </div>
      <Pagination/>
    </div>  <!-- wrapper -->
  </div>   <!--contentEvent -->
</template>

<script>
import Item from '@/components/specialComponents/Item'
import Pagination from '@/components/specialComponents/pagination'
export default {
  name: 'EventContent',
  data () {
    return {
      limit: 2,
      data: ['Country', 'Ukraine', 'Spain', 'Region', 'Kievska', 'New York', 'City', 'Kiev', 'Chernivtsi']
    }
  },
  components: {
    Item,
    Pagination
  },
  props: {
    dataItems: Array,
    default: () => []
  },
  computed: {
    computedObj () {
      var f = this.data.slice(0, 3)
      var r = this.data.slice(3, 6)
      var t = this.data.slice(6, 9)
      return (f, r, t)
    }
  }
}
</script>
<style lang="scss">
.contentEvent {
  background-color: $dark;
  &__title {
    text-align: center;
    padding: rem(20) 0 rem(45);
    color: $white;
    font-style: normal;
    font-weight: 500;
    font-size: rem(52);
    line-height: 63px;
  }
  &__filters {
    @include FCenter(space-between);
    width: rem(350);
  }
  &__filterItem {
    position: relative;
  }
  &__select {
    cursor: pointer;
    outline: none;
    color: $white;
    font-size: rem(20);
    background: none;
    border: none;
    appearance: none;
  }
  &__items {
    @include FCenter(space-between);
    flex-wrap: wrap;
    padding: rem(40) 0;
  }
}
</style>
