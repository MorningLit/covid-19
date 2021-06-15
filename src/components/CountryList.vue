<template>
  <div v-if="!countries"><h1>Loading</h1></div>
  <div
    v-else
    v-for="country in countries"
    :key="country.name"
    class="country-wrapper"
  >
    <div class="flag-wrapper">
      <img
        v-bind:src="
          'https://www.countryflags.io/' + country.code + '/flat/64.png'
        "
      />
    </div>
    <a>
      {{ country.name }}
    </a>
  </div>
</template>

<script>
  export default {
    name: "CountryList",
    props: ["countries"],
  };
</script>

<style>
  .country-wrapper {
    border: 2px solid black;
    border-radius: 16px;
    height: 20vh;
    margin-left: 10px;
    margin-right: 10px;
  }
  .flag-wrapper {
    width: 64px;
    margin: auto;
  }
  .country-wrapper a {
    display: block;
    width: 200px;
    text-align: center;
  }
  .country-wrapper:hover {
    background: #d9dddc;
    cursor: pointer;
  }
</style>
