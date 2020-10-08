<template>
  <tr>
    <td>
      {{ day }}
      {{ weather.temperature }} °
    </td>
    <td>
      <img
        v-if="weather"
        :src="weatherImages"
        alt="weather
      image"
      />
    </td>
  </tr>
</template>

<script>
import dayjs from "dayjs";
export default {
  name: "ForecastDay",
  props: {
    weather: Object
  },
  computed: {
    weatherImages() {
      const futureWeather = this.weather.condition.toLowerCase();
      return require(`../assets/${futureWeather}.png`);
    },
    day() {
      return dayjs(this.weather.day).format("dddd MMM");
    }
  }
};
</script>

<style lang="scss" scoped>
tr,
td {
  text-align: center;
  padding: 0.5em;
}
</style>
