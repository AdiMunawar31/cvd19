<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <h3 class="text-2xl mt-10 font-bold">SELECT COUNTRY :</h3>
    <CountryS @get-country="getCountry" :countries="countries" />

    <button
      @click="clearCountry"
      class="bg-gradient-to-r from-green-400 to-blue-500 hover:from-pink-500 hover:to-yellow-500 mb-7 p-2 rounded"
      v-if="stats.Country"
    >
      Clear Country
    </button>

    <Footer />
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-100 text-4xl mt-20 mb-20 font-bold">
      Fetching Data
    </div>
    <img :src="loadingImage" alt="load image" class="w-24 m-auto" />
  </main>
</template>

<script>
// @ is an alias to /src
import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountryS from "@/components/CountryS.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "Home",
  components: {
    Footer,
    CountryS,
    DataBoxes,
    DataTitle,
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/load.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = res.json();
      return data;
    },
    getCountry(country) {
      (this.stats = country), (this.title = country.Country);
    },
    async clearCountry() {
      this.loading = true;
      const data = await this.fetchCovidData();
      (this.title = "Global"),
        (this.stats = data.Global),
        (this.loading = false);
    },
  },
  async created() {
    const data = await this.fetchCovidData();

    (this.dataDate = data.Date),
      (this.stats = data.Global),
      (this.countries = data.Countries),
      (this.loading = false);
  },
};
</script>
