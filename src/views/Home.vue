<template>
  <div :class="darkMode ? 'dark' : ''">
    <div class="top-section">
      <WorldStatistics
        :worldStats="worldStats"
        :countryStats="countryStats"
        @display-world="displayWorld"
        :toggleDark="toggleDark"
      />
    </div>
    <div class="middle-section">
      <input type="text" v-model="search" placeholder="Search countries..." />
      <div>
        <label>Sort by: </label>
        <select v-model="sort"
          ><option>A-Z</option
          ><option>Z-A</option></select
        >
      </div>
    </div>
    <div class="bottom-section">
      <CountryList
        :countries="filteredCountries"
        @display-country="changeStats"
      />
    </div>
  </div>
</template>

<script>
  import CountryList from "../components/CountryList.vue";
  import WorldStatistics from "../components/WorldStatistics.vue";
  import axios from "axios";

  export default {
    name: "App",
    components: { CountryList, WorldStatistics },
    data() {
      return {
        countries: [],
        worldStats: null,
        countryStats: null,
        search: "",
        sort: "A-Z",
        darkMode: false,
      };
    },
    methods: {
      changeStats(stats) {
        axios.get(`https://corona-api.com/countries/${stats}`).then((res) => {
          this.countryStats = res.data.data;
        });
      },
      displayWorld() {
        this.countryStats = null;
      },
      toggleDark() {
        this.darkMode = !this.darkMode;
      },
    },
    computed: {
      filteredCountries: function() {
        switch (this.sort) {
          case "A-Z":
            return [...this.countries].sort().filter((country) => {
              return country.name
                .toLowerCase()
                .match(this.search.toLowerCase());
            });
          case "Z-A":
            return [...this.countries]
              .sort()
              .reverse()
              .filter((country) => {
                return country.name
                  .toLowerCase()
                  .match(this.search.toLowerCase());
              });
          default:
            return [...this.countries].sort().filter((country) => {
              return country.name
                .toLowerCase()
                .match(this.search.toLowerCase());
            });
        }
      },
    },
    mounted() {
      axios.get("https://corona-api.com/countries").then((res) => {
        this.countries = res.data.data;
      });
      axios.get("https://corona-api.com/timeline").then((res) => {
        this.worldStats = res.data.data[0];
      });

      const target = document.querySelector(".bottom-section");

      target.addEventListener("wheel", (event) => {
        const toLeft = event.deltaY < 0 && target.scrollLeft > 0;
        const toRight =
          event.deltaY > 0 &&
          target.scrollLeft < target.scrollWidth - target.clientWidth;

        if (toLeft || toRight) {
          event.preventDefault();
          target.scrollLeft += event.deltaY;
        }
      });
    },
  };
</script>

<style>
  body {
    margin: 0;
    font-family: "Lora", serif;
  }
  #app {
    display: flex;
    flex-direction: column;
  }
  .top-section {
    height: 66vh;
    overflow-y: auto;
  }
  .middle-section {
    height: 4vh;
    margin-left: 10px;
    margin-right: 10px;
    display: flex;
    justify-content: space-between;
  }
  .bottom-section {
    height: 30vh;
    overflow: auto;
    display: flex;
    align-items: center;
  }

  .dark {
    background: #192734;
    color: #f3f3f3;
  }
  .dark .country-wrapper:hover {
    background: #000;
  }
</style>
