<template>
  <section class="Filters">
    <div class="Filters__box">
    <Select :defaultItem="'Country'"
            :selected="selected.countries"
            :items="dataFilter.countries"
            :select="select('countries')"
            @selectedOpion="snowFilter"
    />
    <Select :defaultItem="'Region'"
            :selected="selected.regions"
            :items="dataFilter.regions"
            :select="select('regions')"
            @selectedOpion="snowFilter"
    />
    <Select :defaultItem="'City'"
            :selected="selected.cities"
            :items="dataFilter.cities"
            :select="select('cities')"
            @selectedOpion="snowFilter"
    />
    </div>
    <!-- :hideOptions="hideFilter" -->
      <p class="Filters__filter" v-if="showCFilter" @click="hideFilter">{{filter}}</p>
  </section>
</template>
<script>
import Select from '@/components/specialComponents/Select'
export default {
  name: 'Filters',
  components: {
    Select
  },
  data () {
    return {
      selected: {
        countries: 0,
        regions: 0,
        cities: 0
      },
      showCFilter: false,
      filter: 'Clear Filters'
    }
  },
  props: {
    dataFilter: Object
  },
  methods: {
    snowFilter (id) {
      if (id > 0) {
        this.showCFilter = true
      } else {
        this.showCFilter = false
      }
    },
    hideFilter (id) {
      this.showCFilter = false
      id = 0
      return id
    },
    select (key) {
      return (id) => {
        this.selected[key] = id
      }
    },
    selectDefault: () => {
      Object.keys(this.selected).map(key => this.select(key)(0))
    }
  },
  mounted () {
    this.select = this.select.bind(this)
  }
}
</script>
<style lang="scss">
.Filters {
  @include FCenter(flex-start);
  &__box {
    @include FCenter(space-between);
    width: rem(450);
  }
  &__filter {
    margin-left: rem(10);
    cursor: pointer;
    color: $white;
    font-size: rem(20);
  }
}
</style>
