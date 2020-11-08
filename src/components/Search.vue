<template>
  <div class="cities">
    <div>Ville : {{ city }}</div>
    <div>Temperature : {{ todayTemp }}</div>
  </div>
</template>

<script>
export default {
  name: "Search",
  data: () => ({
    city: "",
    todayTemp: 0
  }),
  created() {
    this.cities();
  },
  watch: {
    $route: "cities"
  },
  methods: {
    cities() {
      fetch(
        `https://api.openweathermap.org/data/2.5/forecast?q=${this.$route.query.city}&appid=${process.env.VUE_APP_OPEN_WEATHER_API}&units=metric`
      )
        .then(response => response.json())
        .then(data => {
          this.todayTemp = Math.round(data.list[0].main.temp_max);
          this.city = data.city.name;
          console.log(data);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.cities {
  height: 90vh;
  display: flex;
  flex-direction: column;
  text-align: center;
  #research {
    background: transparent;
    border: 1px solid lightgrey;
    border-radius: 4px;
    color: white;
  }
}
</style>
