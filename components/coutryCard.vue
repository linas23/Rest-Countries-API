<template>
  <v-card hover class="pb-3" color="grey lighten-5" @click="showMyCountry(country.name)">
    <v-img :src="country.flag" max-height="177px" contain></v-img>
    <v-card-title class="title">{{country.name}}</v-card-title>
    <v-card-text class="subtitle-1 py-0">
      Population :
      <span class="secondary--text font-weight-medium">{{country.population | formatIt}}</span>
    </v-card-text>
    <v-card-text class="subtitle-1 py-0">
      Region:
      <span class="secondary--text fon t-weight-medium">{{country.region}}</span>
    </v-card-text>
    <v-card-text class="subtitle-1 py-0">
      Capital:
      <span class="secondary--text font-weight-medium">{{country.capital}}</span>
    </v-card-text>
  </v-card>
</template>

<script>
import numeral from "numeral";
export default {
  props: {
    country: {
      type: Object,
      required: true
    }
  },
  filters: {
    formatIt: function(value) {
      return numeral(value).format();
      // return value.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,");
    }
  },
  methods: {
    showMyCountry(name) {
      this.$router.push({
        path: `/country/${name}`
      });
    }
  }
};
</script>

<style>
</style>