<template>
  <div class="Pagination">
<!--         <li class="Pagination__item">
          <div type="button" class="Pagination__prev" @click="page--"></div>
        </li>
        <li class="Pagination__item">
          <button type="button" class="Pagination__number" v-for="pageNumber in pages.slice(page-1, page+2)" @click="page = pageNumber"> {{pageNumber}} </button>
        </li>
        <li class="Pagination__item">
          <div type="button" @click="page++" v-if="page < pages.length" class="Pagination__next"></div>
        </li> -->
  </div>
</template>

<script>
export default {
  name: 'Pagination',
  data () {
    return {
      posts: [''],
      page: 1,
      perPage: 10,
      pages: []
    }
  },
  methods: {
    // getPosts () {
    //   let data = [];
    //   for (let i = 0; i < 200; i++) {
    //     this.posts.push({first: 'John',last:'Doe', suffix:'#' + i})
    //   }
    // },
    setPages () {
      const numberOfPages = Math.ceil(this.posts.length / this.perPage)
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index)
      }
    },
    paginate (posts) {
      const page = this.page
      const perPage = this.perPage
      const from = (page * perPage) - perPage
      const to = (page * perPage)
      return posts.slice(from, to)
    }
  },
  computed: {
    displayedPosts () {
      return this.paginate(this.posts)
    }
  },
  watch: {
    posts () {
      this.setPages()
    }
  },
  created () {
    this.getPosts()
  }
  // filters: {
  //   trimWords(value){
  //     return value.split(" ").splice(0,20).join(" ") + '...';
  //   }
  // }
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
}
</style>
