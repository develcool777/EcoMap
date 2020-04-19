<template>
  <div class="Select">
    <div tabindex="0" class="Select__selected" @click="clicked()">{{selectedItem().name}}</div>
    <span class="Select__box" v-if="show">
      <p class="Select__option" v-if="itemByDefault()"  @click="selectItem(0)">{{defaultItem}}</p>
      <p class="Select__option" v-for="({id, name}, i) in items" :key="i" @click="selectItem(id)">{{name}}</p>
    </span>
  </div>
</template>
<script>
export default {
  name: 'Select',
  data () {
    return {
      show: false
    }
  },
  props: {
    defaultItem: String,
    selected: Number,
    items: Array,
    select: Function
  },
  methods: {
    itemByDefault () {
      return this.selected > 0
    },
    selectedItem () {
      const item = this.items.find(item => item.id === this.selected) || {
        id: 0,
        name: this.defaultItem
      }
      return item
    },
    clicked () {
      this.show = !this.show
    },
    selectItem (id) {
      this.select(id)
      this.show = false
    },
    hide () {
      this.show = false
    }
  },
  mounted () {
    this.hide = this.hide.bind(this)
    this.clicked = this.clicked.bind(this)
    this.selectedItem = this.selectedItem.bind(this)
    this.selectItem = this.selectItem.bind(this)
    document.addEventListener('click', this.hide, true)
  },
  beforeDestroy () {
    document.removeEventListener('click', this.hide)
  }
}
</script>
<style lang="scss">
.Select {
  font-size: rem(20);
  width: rem(130);
  position: relative;
  &__selected {
    position: relative;
    // width: 92%;
    // margin: rem(5) rem(10) rem(5) rem(10);
    padding: 5px;
    border: none;
    background: transparent;
    font-size: rem(20);
    color: $white;
    text-overflow: ellipsis;
    overflow: hidden;
    transition: color .5s;
  }
  &__selected:after {
    position: absolute;
    content: "";
    top: 50%;
    left: 90%;
    width: 5px;
    height: 5px;
    border-top: 2px solid $white;
    border-left: 2px solid $white;
    transform: rotate(45deg);
    transition-duration: .5s;
  }
  &__selected:focus {
    background: $white;
    color: $red;
    border-radius: 5px 5px 0 0;
    outline: none;
  }
  &__selected:focus:after {
    top: 45%;
    transform: rotate(225deg);
    border-color: $red;
  }
  &__selected:hover {
    cursor: pointer;
    color: $red;
  }
  &__box {
    width: rem(200); // or 100%
    cursor: pointer;
    display: block;
    position: absolute;
    background: $white;
    color: $dark;
    border-radius: 0 5px 5px 5px; // or
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
    border-radius: 0 5px 0 0;
  }
  &__option:last-child {
    border-radius: 0 0 5px 0;
  }
  &__option:hover {
    background-color: $gray;
  }
}
</style>
