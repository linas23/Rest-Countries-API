<template>
  <div>
    <compInput @changeRegion="handleRegionChange" @searchCountry="showMyCountry"></compInput>
    <v-divider></v-divider>
    <v-row>
      <v-col cols="12" sm="6" lg="3" v-for="(country,index) in countries" :key="index">
        <countryCard :country="country"></countryCard>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import countryCard from "../components/coutryCard";
import compInput from "../components/inputs";
export default {
  data() {
    return {
      countries: []
    };
  },
  components: {
    compInput,
    countryCard
  },
  async created() {
    let results = await this.$axios
      .get("https://restcountries.eu/rest/v2/all")
      .then(res => res.data);

    results = results.sort(function() {
      return 0.5 - Math.random();
    });
    this.countries = [...results];
  },
  methods: {
    async handleRegionChange(payload) {
      this.countries = [];
      let countries = await this.$axios.$get(
        `https://restcountries.eu/rest/v2/region/${payload}`
      );
      this.countries = [...countries];
    },
    async showMyCountry(countryName) {
      this.$router.push({
        path: `/country/${countryName}`
      });
    }
  }
};
</script>
