<template>
  <div class="Pagination">
        <li class="Pagination__item">
          <div class="Pagination__prev" v-if="hasPrev()" @click.prevent="changePage(pagePrev())"></div>
        </li>
        <li class="Pagination__item" v-for="(page, i) in pages()" :key="i">
          <button class="Pagination__number" @click.prevent="changePage(page)" :class="{ current: current == page }"> {{ page + 1 }} </button>
        </li>
        <li class="Pagination__item">
          <div class="Pagination__next" v-if="hasNext()" @click.prevent="changePage(pageNext())"></div>
        </li>
  </div>
</template>

<script>
export default {
  name: 'Pagination',
  data () {
    return {}
  },
  props: {
    current: {
      type: Number,
      default: 1
    },
    totalItems: {
      type: Number,
      default: 2
    },
    perPage: {
      type: Number,
      default: 2
    },
    pageRange: {
      type: Number,
      default: 2
    }
  },
  methods: {
    pageFirst () {
      return 0
    },
    pageLast () {
      return this.totalPages()
    },
    pageId () {
      return Math.max(Math.min(this.current, this.pageLast()), this.pageFirst())
    },
    totalPages () {
      return Math.ceil(this.totalItems / this.perPage)
    },
    pageNext () {
      return Math.min(this.pageLast(), this.pageId() + 1)
    },
    pagePrev () {
      return Math.max(this.pageFirst(), this.pageId() - 1)
    },
    pages () {
      return Array.from(Array(2 * this.pageRange + 1), (_, i) => i - this.pageRange + this.pageId())
        .filter(i => this.pageFirst() <= i && i <= this.pageLast())
    },
    // hasFirst: function() {
    //   return this.rangeStart !== 1
    // },
    // hasLast: function() {
    //   return this.rangeEnd < this.totalPages
    // },
    hasPrev () {
      return this.pageId() > this.pageFirst()
    },
    hasNext () {
      return this.pageId() < this.pageLast()
    },
    changePage (page) {
      this.$emit('page-changed', page)
    }
  }
}
</script>
<style lang="scss">
.Pagination {
  width: rem(200);
  @include FCenter(space-between);
  margin: 0 auto;
  padding: rem(30) 0;
  &__item > * {
    background: none;
    color: $white;
    font-size: rem(26);
    border: none;
  }
  &__prev {
    border-style: solid;
    border-width: 5px 10px 5px 0;
    border-color: transparent $white transparent transparent;
    transition-duration: .5s;
  }
  &__next {
    border-style: solid;
    border-width: 5px 0 5px 10px;
    border-color: transparent transparent transparent $white;
    transition-duration: .5s;
  }
  &__prev:hover {
    border-color: transparent $red transparent transparent;
    cursor: pointer;
  }
  &__next:hover {
    border-color: transparent transparent transparent $red;
    cursor: pointer;
  }
  &__number {
    cursor: pointer;
    transition-duration: .5s;
    border-bottom: 1px solid transparent;
  }
  &__number:focus {
    outline: none;
  }
  &__number:hover {
    border-bottom: 1px solid $red;
    color: $red;
  }
}
.current {
  color: $red;
  border-bottom: 1px solid $red;
}
</style>
