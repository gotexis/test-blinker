<template lang="pug">
  section.section
    p.title Browse Used Cars
    br

    .columns
      .column
        label.label Keyword
        b-field
          b-input(
            placeholder="Input make, model or keyword..."
            v-model="searchInput"
            expanded
          )
          .control
            b-button.is-primary Find
      .column
        b-field(label='Buy price')
          b-slider(v-model='priceRange', :min='0', :max='100000', :step='1000' lazy)
    br
    .columns.is-multiline
      .column.is-4(v-for="car in getCarList" :key="car.stock_item_id")
        Card(:car="car")
    b-notification(:closable="false" v-if="carList.length === 0")
      | No result found! Try refining search criteria or keyword?

</template>

<script>
import axios from 'axios';
import qs from 'qs';
import Card from '@/components/Card.vue';

export default {
  components: {
    Card,
  },

  data() {
    return {
      carList: [],
      priceRange: [0, 100000],
    };
  },

  computed: {
    getCarList() {
      return this.carList.filter(x => !!x.stock_item_id);
    },
  },

  watch: {
    '$route.query.q': function () {
      this.load();
    },
    priceRange() {
      this.load();
    },
  },

  methods: {
    research() {
      this.$router.push({
        name: 'search',
        query: {
          q: this.searchInput,
        },
      }).catch((e) => {});
    },
    async load() {
      const response = await axios.get('https://api.testing.hellocars.com.au/buy/search', {
        params: {
          query: this.searchInput.replace(' ', '+'),
          'price[]': [this.priceRange[0], this.priceRange[1]],
        },
        paramsSerializer: params => qs.stringify(params, { arrayFormat: 'brackets' }).replace(/%2B/g, '+').replace(/%5B/g, '[').replace(/%5D/g, ']')
          .replace(/\[]\[]/g, '[]'),
      });
      this.carList = response.data.data;
      console.log(this.carList);
    },
  },

  mounted() {
    this.searchInput = this.$route.query.q;
    this.load();
  },

};
</script>

<style lang="sass" scoped>
  .list-switch
    /* Ensure it wont be too far right so button shakes */
    min-width: 10rem

</style>
