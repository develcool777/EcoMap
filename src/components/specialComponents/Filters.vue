<template>
  <section class="Filters">
    <div class="Filters__box">
    <Select :defaultItem="'Country'"
            :selected="selected.countries"
            :items="dataFilter.countries"
            :select="select('countries')"
    />
    <Select :defaultItem="'Region'"
            :selected="selected.regions"
            :items="dataFilter.regions"
            :select="select('regions')"
    />
    <Select :defaultItem="'City'"
            :selected="selected.cities"
            :items="dataFilter.cities"
            :select="select('cities')"
    />
    <Select :defaultItem="'Problem'"
            :selected="selected.problems"
            :items="dataFilter.problems"
            :select="select('problems')"
    />
    </div>
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
        cities: 0,
        problems: 0
      },
      showCFilter: false,
      filter: 'Clear Filters'
    }
  },
  props: {
    dataFilter: Object
  },
  methods: {
    hideFilter () {
      this.showCFilter = false
      this.selected.countries = 0
      this.selected.regions = 0
      this.selected.cities = 0
      this.selected.problems = 0
    },
    select (key) {
      return (id) => {
        this.selected[key] = id
        this.showCFilter = Object.values(this.selected).some(i => i)
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
    // width: rem(450);
  }
  &__filter {
    margin-left: rem(10);
    color: $white;
    font-size: rem(20);
    transition-duration: .5s;
  }
  &__filter:hover {
    cursor: pointer;
    color: $red;
  }
}
</style>
