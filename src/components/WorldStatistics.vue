<template>
  <div v-if="!worldStats"><h1>Loading</h1></div>
  <div v-else class="wrapper">
    <div class="title">
      <h3>ACTIVE: {{ worldStats.active }}</h3>
      <h1><b>COVID-19 Statistics</b></h1>
      <h2>{{ worldStats.date }}</h2>
    </div>
    <div>
      <div class="new-cases">
        <h2 class="deaths">NEW DEATHS: {{ worldStats.new_deaths }}</h2>
        <h2 class="confirmed">NEW CONFIRMED: {{ worldStats.new_confirmed }}</h2>
        <h2 class="recovered">NEW RECOVERED: {{ worldStats.new_recovered }}</h2>
      </div>
      <div class="total-cases">
        <h3 class="deaths">DEATHS: {{ worldStats.deaths }}</h3>
        <h3 class="confirmed">CONFIRMED: {{ worldStats.confirmed }}</h3>
        <h3 class="recovered">RECOVERED: {{ worldStats.recovered }}</h3>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "WorldStatistics",
    props: ["worldStats"],
  };
</script>

<style>
  .title {
    display: flex;
    justify-content: space-between;
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
