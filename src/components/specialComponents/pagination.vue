<template>
  <div class="Pagination">
        <li class="Pagination__item">
          <div class="Pagination__prev" v-if="hasPrev()" @click.prevent="changePage(prevPage)"></div>
        </li>
        <li class="Pagination__item" v-for="(page, i) in pages" :key="i">
          <button class="Pagination__number" @click.prevent="changePage(page)" :class="{ current: current == page }"> {{ page }} </button>
        </li>
        <li class="Pagination__item">
          <div class="Pagination__next" v-if="hasNext()" @click.prevent="changePage(nextPage)"></div>
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
    total: {
      type: Number,
      default: 0
    },
    perPage: {
      type: Number,
      default: 9
    },
    pageRange: {
      type: Number,
      default: 1
    }
  },
  computed: {
    pages () {
      var pages = []

      for (var i = this.rangeStart; i <= this.rangeEnd; i++) {
        pages.push(i)
      }
      return pages
    },
    rangeStart () {
      var start = this.current - this.pageRange

      return (start > 0) ? start : 1
    },
    rangeEnd () {
      var end = this.current + this.pageRange

      return (end < this.totalPages) ? end : this.totalPages
    },
    totalPages () {
      return Math.ceil(this.total / this.perPage)
    },
    nextPage () {
      return this.current + 1
    },
    prevPage () {
      return this.current - 1
    }
  },
  methods: {
    // hasFirst: function() {
    //   return this.rangeStart !== 1
    // },
    // hasLast: function() {
    //   return this.rangeEnd < this.totalPages
    // },
    hasPrev () {
      return this.current > 1
    },
    hasNext () {
      return this.current < this.totalPages
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
  }
}
.current {
  border-color: #ea4c89;
  color: #ea4c89;
}
</style>
