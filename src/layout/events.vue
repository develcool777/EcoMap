<template>
  <div class="contentEvent">
    <div class="wrapper">
      <div class="contentEvent__title">
        <p>Events</p>
        <svg @click="show" class="contentEvent__svg" viewBox="0 0 30 30" xmlns="http://www.w3.org/2000/svg">
          <path d="M17.5 12.5H30V17.5H17.5V30H12.5V17.5H0V12.5H12.5V0H17.5V12.5Z" />
        </svg>
      </div>
        <Filters :dataFilter="dataFilter"/>
      <div class="contentEvent__items" :style="{height: (orderDataPicker() * 240) + 'px'}">
        <DataPicker :style="{order: orderDataPicker()}" :value="value" :render="render" :start="start" :end="end" :onSelect="onSelect" />
        <Item v-for="(item, i) in dataItems" :key="i" :fitem="item" :style="{order: orderItem(i)}"/>
      </div>
    </div>  <!-- wrapper -->
    <transition name="fade" appear>
    <div class="contentEvent__mask" v-if="active" @click.self="show">
      <form action="post" class="contentEvent__modal">
        <div class="contentEvent__blocks">
          <div class="contentEvent__titleModal">Add new event</div>
          <svg @click="show" class="contentEvent__svg contentEvent__svg--close" viewBox="0 0 30 30" xmlns="http://www.w3.org/2000/svg">
            <path d="M17.5 12.5H30V17.5H17.5V30H12.5V17.5H0V12.5H12.5V0H17.5V12.5Z" />
          </svg>
          <div class="contentEvent__block">
            <div class="contentEvent__item">
              <label class="contentEvent__label" for="issue">Issue</label>
              <div class="contentEvent__div">
                <input type="text" v-model="Issue" class="contentEvent__input" id="issue">
              </div>
            </div>
            <div class="contentEvent__item">
              <label class="contentEvent__label" for="Start time">Start time</label>
              <div class="contentEvent__div">
                <input type="text" v-model="StartTime" class="contentEvent__input" id="Start time">
              </div>
            </div>
            <div class="contentEvent__item">
              <label class="contentEvent__label" for="End time">End time</label>
              <div class="contentEvent__div">
                <input type="text" v-model="EndTime" class="contentEvent__input" id="End time">
              </div>
            </div>
            <div class="contentEvent__item">
              <label class="contentEvent__label" for="Place">Place</label>
              <div class="contentEvent__div">
                <input type="text" v-model="Place" class="contentEvent__input" id="Place">
              </div>
            </div>
            <div class="contentEvent__item">
              <label class="contentEvent__label" for="Max participants">Max participants</label>
              <div class="contentEvent__div">
                <input type="text" v-model="MaxParticipants" class="contentEvent__input" id="Max participants">
              </div>
            </div>
            <div class="contentEvent__item">
              <label class="contentEvent__label" for="Describe problem">Describe problem</label>
              <div class="contentEvent__div">
                <input type="text" v-model="DescribeProblem" class="contentEvent__input" id="Describe problem">
              </div>
            </div>
          </div>
          <div class="contentEvent__btn" @click="addEvent">Add event</div>
        </div>
      </form>
     </div>
   </transition>
  </div>   <!--contentEvent -->
</template>
<script>
import axios from 'axios'
import moment from 'moment'
import Item from '@/components/specialComponents/Item'
import Filters from '@/components/specialComponents/Filters'
import DataPicker from '@/components/specialComponents/dataPicker'
const baseURL = 'http://localhost:3000/Events'
export default {
  name: 'EventContent',
  data () {
    return {
      value: moment().locale('en'),
      start: null,
      end: null,
      active: false,
      Issue: '',
      StartTime: '',
      EndTime: '',
      Place: '',
      MaxParticipants: '',
      DescribeProblem: '',
      Events: ''
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
  async created () {
    try {
      const res = await axios.get(baseURL)

      this.Events = res.data
    } catch (e) {
      console.error(e)
    }
  },
  methods: {
    async addEvent () {
      const res = await axios.post(baseURL, {
        Issue: this.Issue,
        StartTime: this.StartTime,
        EndTime: this.EndTime,
        Place: this.Place,
        MaxParticipants: this.MaxParticipants,
        DescribeProblem: this.DescribeProblem
      })
      this.Events = [...this.Events, res.data]
      this.Issue = ''
      this.StartTime = ''
      this.EndTime = ''
      this.Place = ''
      this.MaxParticipants = ''
      this.DescribeProblem = ''
    },
    show () {
      this.active = !this.active
    },
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
  &__svg {
    position: absolute;
    top: 45%;
    right: 0;
    margin-top: -15px;
    height: rem(30);
    transition-duration: .5s;
    fill: $white;
    &--close {
      top: 2%;
      right: 2%;
      height: rem(20);
      transform: rotate(45deg);
    }
  }
  &__svg:hover {
    fill: $red;
    cursor: pointer;
    transform: rotate(360deg);
  }
  &__svg--close:hover {
    transform: rotate(225deg);
  }
  &__titleModal, &__title {
    color: $white;
    font-style: normal;
    font-weight: 500;
    font-size: rem(52);
    line-height: 63px;
    text-align: center;
  }
  &__title {
    position: relative;
    padding: rem(20) 0 rem(45);
  }
  &__items {
    display: flex;
    align-content: space-between;
    flex-direction: column;
    flex-wrap: wrap;
    padding: rem(40) 0;
  }
  &__mask {
    display: block;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.1);
  }
  &__modal {
    margin: rem(50) auto 0;
    padding: rem(20) 0 rem(40);
    width: rem(600);
    height: rem(640);
    background-color: black;
    z-index: 2;
  }
  &__blocks {
    position: relative;
  }
  &__block {
    width: rem(400);
    margin: rem(20) auto 0;
  }
  &__item {
    width: 50%;
    display: flex;
    flex-direction: column;
  }
  &__item:nth-child(n+1) {
    margin-top: rem(15);
  }
  &__label {
    font-style: normal;
    font-weight: normal;
    font-size: rem(20);
    color: $white;
  }
  &__div {
    border-bottom: 1px solid $white;
    height: 20px;
  }
  &__input {
    color: $white;
    background-color: transparent;
    box-sizing: border-box;
    width: 100%;
    height: 100%;
    outline: none;
    border: none;
    padding: 0;
  }
  &__item:last-child {
    width: 100%;
  }
  &__btn {
    width: rem(112);
    margin: rem(100) auto 0;
    padding: rem(8) rem(94);
    border: 2px solid $white;
    color: $white;
    text-align: center;
    font-size: rem(20);
    transition-duration: .5s;
  }
  &__btn:hover {
    background-color: $white;
    color: black;
    cursor: pointer;
  }
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
