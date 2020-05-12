<template>
  <div>
    <v-btn class="ma-5" tile to="/">
      <v-icon left>mdi-arrow-left</v-icon>Back
    </v-btn>
    <v-row>
      <v-col cols="12" md="6" class="px-0 px-sm-10">
        <v-img height="444" contain :src="country.flag"></v-img>
      </v-col>
      <v-col cols="12" sm="5">
        <v-row>
          <div class="display-2 font-weight-bold">{{country.name}}</div>
        </v-row>
        <v-row class="pa-0">
          <v-col cols="12" md="6" class="px-0">
            <div class="font-weight-medium mb-3">
              Native Name :
              <span class="font-weight-normal secondary--text">{{country.nativeName}}</span>
            </div>
            <div class="font-weight-medium mb-3">
              Population :
              <span class="font-weight-normal secondary--text">{{country.population}}</span>
            </div>
            <div class="font-weight-medium mb-3">
              Region :
              <span class="font-weight-normal secondary--text">{{country.region}}</span>
            </div>
            <div class="font-weight-medium mb-3">
              Sub Region :
              <span class="font-weight-normal secondary--text">{{country.subregion}}</span>
            </div>
            <div class="font-weight-medium mb-3">
              Capital :
              <span class="font-weight-normal secondary--text">{{country.capital}}</span>
            </div>
          </v-col>
          <v-col cols="12" md="6" class="px-0">
            <div class="font-weight-medium mb-3">
              Currencies :
              <span v-for="(c,index) in country.currencies" :key="index">
                <span class="font-weight-normal secondary--text">{{c.name}} {{c.name ? (c.code):''}}</span>
              </span>
            </div>
            <div class="font-weight-medium mb-3">
              Languages :
              <span v-for="(c,index) in country.languages" :key="index">
                <span class="font-weight-normal secondary--text">{{c.name}} ({{c.nativeName}})</span>
              </span>
            </div>
            <div class="font-weight-medium mb-3">
              Also known as :
              <span v-for="(c,index) in country.altSpellings" :key="index">
                <br />
                <span class="font-weight-normal secondary--text">{{c}}</span>
              </span>
            </div>
          </v-col>
        </v-row>
        <v-row class="mt-12">
          <div class="title mr-3">Border Countries :</div>
          <div v-if="country.borders">
            <span v-for="(nei,index) in country.borders" :key="index">
              <v-btn class="ma-2" color="primary" @click="goToNeighbour(nei)">{{nei }}</v-btn>
            </span>
          </div>
          <div v-else>None</div>
        </v-row>
      </v-col>
    </v-row>
    <!-- <googleMap></googleMap> -->
  </div>
</template>

<script>
// import googleMap from "~/components/map.vue";
export default {
  data() {
    return {
      country: {}
      // loading: false
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      let countryName = this.$route.params.name;
      this.country = await this.$axios
        .$get(`https://restcountries.eu/rest/v2/name/${countryName}`)
        .then(res => res[0]);
    },
    async goToNeighbour(name) {
      let country = await this.$axios.$get(
        `https://restcountries.eu/rest/v2/alpha/${name}`
      );
      this.$router.push(`/country/${country.name}`);
      this.country = country;
    }
  }
};
</script>

