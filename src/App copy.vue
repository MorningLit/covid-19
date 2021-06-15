<template>
  <div class="top-section">
    <WorldStatistics :worldStats="worldStats" />
  </div>
  <div class="bottom-section">
    <CountryList :countries="countries" />
  </div>
</template>

<script>
  import CountryList from "./components/CountryList.vue";
  import WorldStatistics from "./components/WorldStatistics.vue";
  import axios from "axios";

  export default {
    name: "App",
    components: { CountryList, WorldStatistics },
    data() {
      return {
        countries: null,
        worldStats: null,
      };
    },
    mounted() {
      axios.get("https://corona-api.com/countries").then((res) => {
        this.countries = res.data.data;
        console.log(res.data.data);
      });
      axios.get("https://corona-api.com/timeline").then((res) => {
        this.worldStats = res.data.data[0];
      });

      const target = document.querySelector(".bottom-section");
      console.log(target);

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
    height: 70vh;
    overflow-y: auto;
  }
  .bottom-section {
    height: 30vh;
    overflow: auto;
    display: flex;
    align-items: center;
  }
</style>
