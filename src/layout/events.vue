<template>
  <div class="contentEvent">
    <div class="wrapper">
      <div class="contentEvent__title">Events</div>
        <Filters :dataFilter="dataFilter"/>
      <div class="contentEvent__items">
        <Item v-for="(item, index) in dataItems"  :key="index" :fitem="item"/>
      </div>
    </div>  <!-- wrapper -->
  </div>   <!--contentEvent -->
</template>
<script>
import Item from '@/components/specialComponents/Item'
import Filters from '@/components/specialComponents/Filters'
export default {
  name: 'EventContent',
  data () {
    return {
    }
  },
  components: {
    Item,
    Filters
  },
  props: {
    dataItems: Array,
    dataFilter: Object
  }
}
</script>
<style lang="scss">
.contentEvent {
  &__title {
    text-align: center;
    padding: rem(20) 0 rem(45);
    color: $white;
    font-style: normal;
    font-weight: 500;
    font-size: rem(52);
    line-height: 63px;
  }
  &__items {
    @include FCenter(space-between);
    flex-wrap: wrap;
    padding: rem(40) 0;
  }
}
</style>
