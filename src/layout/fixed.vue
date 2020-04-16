<template>
  <div class="contentFixed">
    <div class="wrapper">
      <div class="contentFixed__title">Fixed issues</div>
      <div class="contentFixed__filters">
        <Select  @selectedOption1="optionSelected"
                 @selectedOption2="optionSelected"
                 @selectedOption3="optionSelected"
                  :dataFilter="datas"/>
        <p class="contentFixed__filter" v-if="showCFilter" >{{filter}}</p>
      </div>
      <div class="contentFixed__items">
        <Item v-for="(item, index) in dataItems"  :key="index" :fitem="item"/>
      </div>
    </div>  <!-- wrapper -->
  </div>   <!-- contentFixed -->
</template>

<script>
import Item from '@/components/specialComponents/Item'
import Select from '@/components/specialComponents/Select'
export default {
  name: 'FixedContent',
  data () {
    return {
      showCFilter: false,
      filter: 'Clear Filters'
    }
  },
  props: {
    dataItems: Array,
    datas: Object,
    default: () => []
  },
  components: {
    Item,
    Select
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
