<template>
  <div v-if="!worldStats"><h1>Loading</h1></div>
  <div v-else class="wrapper">
    <div class="title">
      <div class="date-about-wrapper">
        <router-link to="/about" class="about-link"><h4>About</h4></router-link
        >&nbsp;&nbsp;
        <h2>{{ worldStats.date }}</h2>
      </div>
      <h1><b>COVID-19 Statistics</b></h1>
      <h3>ACTIVE: {{ numberWithCommas(worldStats.active) }}</h3>
    </div>
    <div>
      <div class="new-cases">
        <h2 class="deaths">
          NEW DEATHS: {{ numberWithCommas(worldStats.new_deaths) }}
        </h2>
        <h2 class="confirmed">
          NEW CONFIRMED: {{ numberWithCommas(worldStats.new_confirmed) }}
        </h2>
        <h2 class="recovered">
          NEW RECOVERED: {{ numberWithCommas(worldStats.new_recovered) }}
        </h2>
      </div>
      <div class="total-cases">
        <h3 class="deaths">
          DEATHS: {{ numberWithCommas(worldStats.deaths) }}
        </h3>
        <h3 class="confirmed">
          CONFIRMED: {{ numberWithCommas(worldStats.confirmed) }}
        </h3>
        <h3 class="recovered">
          RECOVERED: {{ numberWithCommas(worldStats.recovered) }}
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "WorldStatistics",
    props: ["worldStats"],
    methods: {
      numberWithCommas(x) {
        return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      },
    },
  };
</script>

<style>
  .title {
    display: flex;
    justify-content: space-between;
    padding: 0 8px;
  }
  .date-about-wrapper {
    display: flex;
  }
  .about-link {
    margin: auto;
  }
  .wrapper {
    display: flex;
    flex-direction: column;
    height: 100%;
    justify-content: space-between;
  }
  .new-cases {
    display: flex;
    justify-content: space-evenly;
  }
  .total-cases {
    display: flex;
    justify-content: space-around;
  }
  .deaths {
    color: darkred;
  }
  .confirmed {
    color: darkblue;
  }
  .recovered {
    color: darkgreen;
  }
</style>
