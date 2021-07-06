<template>
  <div v-if="!Array.isArray(countries) || !countries.length">
    <h1>No country found!</h1>
  </div>
  <div
    v-else
    v-for="country in countries"
    :key="country.name"
    class="country-wrapper"
    @click="$emit('display-country', country.code)"
  >
    <div class="flag-wrapper">
      <img
        v-bind:src="
          'https://www.countryflags.io/' + country.code + '/flat/64.png'
        "
      />
    </div>
    <p>
      {{ country.name }}
    </p>
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
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }
  .flag-wrapper {
    width: 64px;
    margin: 0 auto;
  }
  .country-wrapper p {
    width: 200px;
    text-align: center;
    margin: 0;
  }
  .country-wrapper:hover {
    background: #d9dddc;
    cursor: pointer;
  }
</style>
