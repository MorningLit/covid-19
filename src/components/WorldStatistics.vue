<template>
  <div v-if="!worldStats"><h1>Loading</h1></div>
  <div v-else class="wrapper">
    <div class="title">
      <div class="date-about-wrapper">
        <router-link to="/about" class="about-link"><h4>About</h4></router-link
        >&nbsp;&nbsp;
        <h2>{{ worldStats.date }}</h2>
      </div>
      <h1 class="title-covid" @click="$emit('display-world')">
        <b>COVID-19 Statistics</b>
      </h1>
      <div class="switch-active-wrapper">
        <label class="switch">
          <input type="checkbox" />
          <span class="slider round" @click="toggleDark"></span>
        </label>
        <h3>ACTIVE: {{ numberWithCommas(worldStats.active) }}</h3>
      </div>
    </div>
    <div v-if="!countryStats">
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
    <div v-else class="country-grid">
      <div class="country-name">
        <img
          v-bind:src="
            'https://www.countryflags.io/' + countryStats.code + '/flat/64.png'
          "
        />
        <h1>{{ countryStats.name }}</h1>
      </div>
      <h3 class="country-new">
        Today's new cases: {{ numberWithCommas(countryStats.today.confirmed) }}
      </h3>
      <div></div>
      <h3 class="country-new">
        Today's death: {{ numberWithCommas(countryStats.today.deaths) }}
      </h3>
      <h3 class="deaths country-stats">
        DEATHS: {{ numberWithCommas(countryStats.latest_data.deaths) }}
      </h3>
      <h3 class="confirmed country-stats">
        CONFIRMED: {{ numberWithCommas(countryStats.latest_data.confirmed) }}
      </h3>
      <h3 class="recovered country-stats">
        RECOVERED: {{ numberWithCommas(countryStats.latest_data.recovered) }}
      </h3>
    </div>
  </div>
</template>

<script>
  export default {
    name: "WorldStatistics",
    props: ["worldStats", "countryStats", "toggleDark"],
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
  .title-covid {
    cursor: pointer;
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
    justify-content: space-around;
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
  .country-grid {
    display: grid;
    text-align: center;
  }
  .country-name {
    grid-column-start: 1;
    grid-column-end: 4;
  }
  .country-name h1 {
    margin-top: 0;
  }
  .country-name img {
    width: 100px;
  }
  .switch-active-wrapper {
    display: flex;
  }
  /* The switch - the box around the slider */
  .switch {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
    margin-top: 1em;
    margin-right: 16px;
  }

  /* Hide default HTML checkbox */
  .switch input {
    opacity: 0;
    width: 0;
    height: 0;
  }

  /* The slider */
  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    -webkit-transition: 0.4s;
    transition: 0.4s;
  }

  .slider:before {
    position: absolute;
    content: "";
    height: 26px;
    width: 26px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    -webkit-transition: 0.4s;
    transition: 0.4s;
  }

  input:checked + .slider {
    background-color: #2196f3;
  }

  input:focus + .slider {
    box-shadow: 0 0 1px #2196f3;
  }

  input:checked + .slider:before {
    -webkit-transform: translateX(26px);
    -ms-transform: translateX(26px);
    transform: translateX(26px);
  }

  /* Rounded sliders */
  .slider.round {
    border-radius: 34px;
  }

  .slider.round:before {
    border-radius: 50%;
  }
</style>
