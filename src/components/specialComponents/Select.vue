<template>
  <section class="Select">
    <div class="Select__block">
      <div tabindex="0" class="Select__selected" @click="clicked1()">{{selected1}}</div>
      <span class="Select__box" v-if="show1">
        <p class="Select__option" v-for="(opt, i) in options[0]" :key="i" @click="selectOption1(opt)">{{opt}}</p>
      </span>
    </div>
    <div class="Select__block">
      <div tabindex="0" class="Select__selected" @click="clicked2()">{{selected2}}</div>
      <span class="Select__box" v-if="show2">
        <p class="Select__option" v-for="(opt, i) in options[1]" :key="i" @click="selectOption2(opt)">{{opt}}</p>
      </span>
    </div>
      <div class="Select__block">
      <div tabindex="0" class="Select__selected" @click="clicked3()">{{selected3}}</div>
      <span class="Select__box" v-if="show3">
        <p class="Select__option" v-for="(opt, i) in options[2]" :key="i" @click="selectOption3(opt)">{{opt}}</p>
      </span>
    </div>
  </section>
</template>
<script>
export default {
  name: 'Select',
  data () {
    return {
      show1: false,
      show2: false,
      show3: false,
      selected1: 'Country',
      selected2: 'Region',
      selected3: 'City'
    }
  },
  props: {
    dataFilter: Object
  },
  methods: {
    clicked1 () {
      this.show1 = !this.show1
    },
    clicked2 () {
      this.show2 = !this.show2
    },
    clicked3 () {
      this.show3 = !this.show3
    },
    selectOption1 (opt) {
      this.$emit('selectedOption1', opt)
      this.selected1 = opt
      this.show1 = false
    },
    selectOption2 (opt) {
      this.$emit('selectedOption2', opt)
      this.selected2 = opt
      this.show2 = false
    },
    selectOption3 (opt) {
      this.$emit('selectedOption3', opt)
      this.selected3 = opt
      this.show3 = false
    },
    hide () {
      this.show1 = false
      this.show2 = false
      this.show3 = false
    },
    selectDefault () {
      this.selected1 = this.dataFilter.select
      this.selected2 = this.dataFilter.select
      this.selected3 = this.dataFilter.select
    }
  },
  computed: {
    selection () {
      const f = this.dataFilter.select
      const s = this.dataFilter.select
      const t = this.dataFilter.select
      return (f, s, t)
    },
    options () {
      const f = this.dataFilter.option.slice(0, 2)
      const s = this.dataFilter.option.slice(2, 4)
      const t = this.dataFilter.option.slice(4, 6)
      return [f, s, t]
    }
  },
  mounted () {
    document.addEventListener('click', this.hide.bind(this), true)
  },
  beforeDestroy () {
    document.removeEventListener('click', this.hide)
  }
}
</script>
<style lang="scss">
.Select {
  @include FCenter(space-between)
  outline: none;
  width: rem(400);
  &__block {
    font-size: rem(20);
    width: rem(120);
    position: relative;
  }
  &__selected {
    font-size: rem(20);
    width: 92%;
    border: none;
    background: transparent;
    color: $white;
    text-overflow: ellipsis;
    overflow: hidden;
    padding: 0 5px;
  }
  &__selected:focus {
    background: $white;
    color: $red;
    border-radius: 5px 5px 0 0;
    outline: none;
  }
  &__box {
    width: 100%;
    cursor: pointer;
    position: absolute;
    background: $white;
    color: $dark;
    border-radius: 0 0 5px 5px;
  }
  &__option {
    text-overflow: ellipsis;
    overflow: hidden;
    padding: 5px;
    transition-duration: .5s;
    border-top: 1px solid $dark;
  }
  &__option:first-child {
    border-top: none;
  }
  &__option:hover {
    background: $gray;
  }
}
</style>
