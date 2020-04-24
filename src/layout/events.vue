<template>
  <div class="contentEvent">
    <div class="wrapper">
      <div class="contentEvent__title">Events</div>
        <Filters :dataFilter="dataFilter"/>
      <div class="contentEvent__items" :style="{height: (orderDataPicker() * 240) + 'px'}">
        <DataPicker :style="{order: orderDataPicker()}" :value="value" :render="render" :start="start" :end="end" :onSelect="onSelect" />
        <Item v-for="(item, i) in dataItems" :key="i" :fitem="item" :style="{order: orderItem(i)}"/>
      </div>
    </div>  <!-- wrapper -->
  </div>   <!--contentEvent -->
</template>
<script>
import moment from 'moment'
import Item from '@/components/specialComponents/Item'
import Filters from '@/components/specialComponents/Filters'
import DataPicker from '@/components/specialComponents/dataPicker'
export default {
  name: 'EventContent',
  data () {
    return {
      value: moment().locale('en'),
      start: null,
      end: null
    }
  },
  components: {
    Item,
    Filters,
    DataPicker
  },
  props: {
    dataItems: Array,
    dataFilter: Object
  },
  methods: {
    now (date) {
      const diff = moment().diff(date, 'hours')
      return diff >= 0 && diff < 24
    },
    render ({ title, date, current }) {
      if (date && date.isValid() && this.now(date)) {
        return `!${title}`
      }
      return title
    },
    onSelect (data) {
      this.value = data
    },
    orderItem (index) {
      const middle = this.orderDataPicker()
      return index < middle ? index : index + 1
    },
    orderDataPicker () {
      return Math.ceil((this.dataItems.length + 2) / 2.0)
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
  &__items {
    display: flex;
    align-content: space-between;
    flex-direction: column;
    flex-wrap: wrap;
    padding: rem(40) 0;
  }
}
</style>
