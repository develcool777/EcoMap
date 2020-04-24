<template>
  <section class="DataPicker">
    <div class="DataPicker__selected">
      <div class="DataPicker__select">26 Oct 2019</div>
      <div class="DataPicker__select">5 Nov 2019</div>
    </div>
    <div class="DataPicker__box">
      <div class="DataPicker__monthes">
        <span class="DataPicker__month" v-for="({title, value, current, date}, index) in monthes()" :class="current ? 'DataPicker__month--current' : ''" :key="index" @click.prevent="select(date)">{{title}}</span>
      </div>
      <div class="DataPicker__week">
        <div class="DataPicker__weekdays">
          <span class="DataPicker__weekprev" @click.prevent="select({offset: -1, unit: 'month'})"></span>
          <p class="DataPicker__weekday" v-for="({title, value, current}, index) in daysOfWeek()" :class="current ? 'DataPicker__weekday--current' : ''" :key="index" >{{title}}</p>
          <span class="DataPicker__weeknext" @click.prevent="select({offset: +1, unit: 'month'})"></span>
        </div>
        <div class="DataPicker__days">
          <p class="DataPicker__day" v-for="({title, value, current, date}, index) in daysOfMonth()" :key="index" @click.prevent="select(date)">{{render ? render({title, date, current}) : title}}</p>
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
    locale: {
      type: String,
      required: false,
      default: 'en'
    },
    value: moment,
    render: {
      type: Function,
      required: true
    },
    start: {
      type: moment,
      required: false
    },
    onSelect: {
      type: Function,
      required: false
    },
    end: {
      type: moment,
      required: false
    }
  },
  methods: {
    monthes () {
      const value = moment(this.value).locale(this.locale)
      return Array(12).fill(value)
        .map((d, i) => moment(d).month(0).add(i, 'months'))
        .map(d => ({
          title: d.format('MMMM'),
          date: d,
          value: d.month(),
          current: d.month() === value.month()
        }))
    },
    daysOfWeek () {
      const value = moment(this.value).locale(this.locale)
      return Array(7).fill(value)
        .map((d, i) => moment(d).weekday(0).add(i, 'days'))
        .map(d => ({
          title: d.format('dd'),
          value: d.weekday(),
          cuurnt: d.weekday() === value.weekday()
        }))
    },
    daysOfMonth () {
      const value = moment(this.value).locale(this.locale)
      const d1 = moment(value).date(1).weekday(0)
      const d2 = moment(value).date(1).add(1, 'month').add(-1, 'days').weekday(0).add(1, 'week')
      return Array(d2.diff(d1, 'days')).fill(d1)
        .map((d, i) => moment(d).add(i, 'days'))
        .map(d => {
          return d.month() === value.month() ? {
            title: d.format('D'),
            date: d,
            value: d.date(),
            current: d.date() === value.date()
          } : {
            date: d
          }
        })
    },
    select (date) {
      if (date instanceof moment) {
        this.onSelect && this.onSelect(date)
      } else if (date instanceof Object) {
        const { offset, unit } = date
        this.select(moment(this.value).add(+offset, unit))
      }
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
  margin-bottom: rem(45);
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
    margin-top: rem(5);
    height: rem(358);
    border: 1px solid $white;
  }
  &__monthes {
    display: flex;
    flex-direction: column;
    width: rem(180);
    overflow-y: scroll;
    border-right: 1px solid $white;
    // padding: rem(10) 0 rem(15) rem(24);
    padding: 0 0 0 rem(24);
  }
  &__monthes::-webkit-scrollbar {
      display: block;
      width: 5px;
  }
  &__monthes::-webkit-scrollbar-track {
      background: none;
  }
  &__monthes::-webkit-scrollbar-thumb {
      background-color: $white;
      border-radius: 10px 0 0 10px;
      border-right: none;
      border-left: none;
  }
  &__month {
    display: inline-block;
    margin-top: rem(15);
    font-size: rem(14);
    color: $white;
    line-height: rem(20);
    transition-duration: .5s;
    cursor: pointer;
    &--current {
      cursor: default;
      font-weight: bold;
      color: $whiter;
    }
  }
  &__month:hover {
    color: $red;
    &--current:hover {
      color: $whiter;
    }
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
// padding-bottom: 5px;
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
    justify-content: space-between;
    flex-wrap: wrap;
    margin: rem(15) auto;
    width: rem(290);
  }
  &__day {
    width: rem(36);
    padding: rem(9) 0;
    border-radius: 50%;
    border: 1px solid transparent;
    margin: rem(5) 0;
    text-align: center;
    font-style: normal;
    font-weight: normal;
    font-size: rem(16);
    line-height: rem(20);
    transition: border-color .5s, background-color .5s;
  }
  &__day:not(:empty):hover {
    cursor: pointer;
    border-color: $white;
    color: black;
    background-color: $white;
  }
}
</style>
