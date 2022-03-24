<template>
  <main v-if="!loading">
    <data-title :text="title" :dataDate="dataDate"></data-title>
    <data-boxes :status="status"></data-boxes>
    <country-select
      :countries="countries"
      @get-country="getCountryData"
    ></country-select>
    <button
      class="bg-green-400 text-white p-3 rounded mt-10"
      @click="clearCountryData()"
    >
      Clear Country
    </button>
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data....</div>
      <img :src="loadingImage" alt="loading" class="w-24 m-auto" />
    </div>
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle.vue";
import DataBox from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";

export default {
  name: "HomeView",
  components: {
    "data-title": DataTitle,
    "data-boxes": DataBox,
    "country-select": CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: "Globel",
      dataDate: "",
      status: {},
      countries: [],
      loadingImage: require("../assets/loading.svg"),
    };
  },
  methods: {
    async covidDataFetch() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country) {
      this.status = country;
      this.title = country.Country;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.covidDataFetch();
      this.title = "Globel";
      this.status = data.Global;
      this.loading = false;
    },
  },
  async created() {
    const data = await this.covidDataFetch();

    this.dataDate = data.Date;
    this.status = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
