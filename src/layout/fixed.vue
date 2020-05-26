<template>
  <div class="contentFixed">
    <div class="wrapper">
      <div class="contentFixed__title">Fixed</div>
        <Filters :dataFilter="dataFilter"/>
      <div class="contentFixed__items">
        <Item v-for="(item, index) in dataItems"  :key="index" :fitem="item"/>
      </div>
    </div>  <!-- wrapper -->
  </div>   <!-- contentFixed -->
</template>

<script>
import Item from '@/components/specialComponents/Item'
import Filters from '@/components/specialComponents/Filters'
export default {
  name: 'FixedContent',
  data () {
    return {
    }
  },
  props: {
    dataItems: Array,
    dataFilter: Object,
    default: () => []
  },
  components: {
    Item,
    Filters
  },
  methods: {
    optionSelected (opt) {
      this.showCFilter = true
    }
  }
}
</script>
<style lang="scss">
.contentFixed {
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
    @include FCenter(flex-start);
  }
  &__filter {
    cursor: pointer;
    color: $white;
    font-size: rem(20);
  }
  &__items {
    @include FCenter(space-between);
    flex-wrap: wrap;
    padding: rem(40) 0;
  }
}
</style>
