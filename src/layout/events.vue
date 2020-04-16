<template>
  <div class="contentEvent">
    <div class="wrapper">
      <div class="contentEvent__title">Events</div>
      <div class="contentEvent__filters">
        <Select  @selectedOption1="optionSelected"
                 @selectedOption2="optionSelected"
                 @selectedOption3="optionSelected"
                  :dataFilter="datas"/>
        <p class="contentEvent__filter" v-if="showCFilter" >{{filter}}</p>
      </div>
      <div class="contentEvent__items">
        <Item v-for="(item, index) in dataItems"  :key="index" :fitem="item"/>
      </div>
    </div>  <!-- wrapper -->
  </div>   <!--contentEvent -->
</template>

<script>
import Item from '@/components/specialComponents/Item'
import Select from '@/components/specialComponents/Select'
export default {
  name: 'EventContent',
  data () {
    return {
      showCFilter: false,
      filter: 'Clear Filters'
    }
  },
  components: {
    Item,
    Select
  },
  props: {
    dataItems: Array,
    datas: Array
  },
  methods: {
    optionSelected (opt) {
      this.showCFilter = true
    }
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
