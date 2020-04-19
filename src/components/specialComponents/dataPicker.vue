<template>
  <section class="DataPicker">
    <div class="DataPicker__selected">
      <div class="DataPicker__select">26 Oct 2019</div>
      <div class="DataPicker__select">5 Nov 2019</div>
    </div>
    <div class="DataPicker__box">
      <div class="DataPicker__monthes">
        <p class="DataPicker__month" v-for="(month, index) in monthes()" :key="index">{{month}}</p>
      </div>
      <div class="DataPicker__week">
        <div class="DataPicker__weekdays">
          <span class="DataPicker__weekprev"></span>
          <p class="DataPicker__weekday" v-for="(weekday, index) in daysOfWeek()" :key="index">{{weekday}}</p>
          <span class="DataPicker__weeknext"></span>
        </div>
        <div class="DataPicker__days">
          <p class="DataPicker__day" v-for="(monthday, index) in daysOfMonth()" :key="index" >{{monthday}}</p>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import moment from 'moment'
export default {
  name: 'DataPicker',
  data () {
    return {
    }
  },
  props: {
    value: moment,
    render: Function,
    start: {
      type: moment,
      required: false
    },
    end: {
      type: moment,
      required: false
    }
  },
  methods: {
    amount (value, of, unit) {
      return -value.diff(moment(value).add(1, of), unit)
    },
    format (value, of, unit, format) {
      return (_, i) => moment(value).startOf(of).add(i, unit).format(format)
    },
    monthes () {
      const monthes = this.amount(this.value, 'year', 'month')
      const format = this.format(this.value, 'year', 'month', 'MMMM')
      return Array.from(Array(monthes), format)
    },
    daysOfWeek () {
      const days = this.amount(this.value, 'week', 'day')
      const format = this.format(this.value, 'week', 'day', 'dd')
      return Array.from(Array(days), format)
    },
    daysOfMonth () {
      const days = this.amount(this.value, 'month', 'day')
      const format = this.format(this.value, 'month', 'day', 'D/w/e')
      let result = Array.from(Array(days), format).reduce((scope, item) => {
        const [day, weekId, dayOfWeek] = item.split('/')
        if (!scope[+weekId]) {
          scope[+weekId] = Array(7).fill('')
        }
        scope[+weekId][+dayOfWeek] = this.render(day, moment(this.value).date(+day))
        return scope
      }, {})
      result = Object.values(result)
      console.log(result)
      result = [].concat(...result)
      return result
    }
  }
}
</script>
<style lang="scss">
.DataPicker {
  font-family: Work Sans;
  display: inline-block;
  font-weight: normal;
  width: rem(560);
  &__selected {
    @include FCenter(flex-start);
    color: $white;
  }
  &__select {
    padding: rem(25) rem(50) rem(25) rem(15);
    border: 1px solid $grayDP;
  }
  &__select:last-child {
    border-color: $white;
    font-weight: bold;
  }
  &__box {
    display: flex;
    height: rem(358);
    border: 1px solid $white;
  }
  &__monthes {
    display: flex;
    flex-direction: column;
    width: rem(180);
    overflow: scroll;
    color: $white;
    border-right: 1px solid $white;
    padding: rem(10) 0 rem(15);
  }
  &__month {
    margin-left: rem(24);
    font-size: rem(14);
  }
  &__month:not(:first-child) {
    margin-top: rem(15);
  }
  &__week {
    display: flex;
    flex-direction: column;
    color: $white;
    padding: rem(10) rem(24) 0;

  }
  &__weekdays {
    @include FCenter(space-between);
    // margin: 5px auto;  what???
    position: relative;
    width: rem(330);
  }
  &__weekdays:after {
    content: "";
    position: absolute;
    bottom: -5px;
    display: block;
    width: 100%;
    height: 1px;
    background: $white;
  }
  &__weekday {
    transition-duration: .5s;
  }
  &__weekday:hover {
    cursor: pointer;
    color: $red;
  }
  &__weekprev, &__weeknext {
    width: 2px;
    height: 2px;
    border-style: solid;
    border-width: 2.5px 5px 2.5px 0;
    border-color: transparent $white transparent transparent;
    transition-duration: .5s;
    cursor: pointer;
  }
  &__weeknext {
    border-width: 2.5px 0 2.5px 5px;
    border-color: transparent transparent transparent $white;
  }
  &__weekprev:hover{
    border-color: transparent $red transparent transparent;
  }
  &__weeknext:hover {
    border-color: transparent transparent transparent $red;
  }
  &__days {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    margin: rem(15) auto;
    width: rem(308);
  }
  &__day {
    width: calc(100%/7);
    font-style: normal;
    font-weight: normal;
    font-size: 16px;

  }
}
</style>
