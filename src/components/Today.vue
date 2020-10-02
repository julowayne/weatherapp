<template>
  <div id="today">
    <div>
      <h1>{{ today }}</h1>
    </div>
    <div id="temp">{{ todayTemp }}°c {{ city }}</div>
    <div>
      <img
        v-if="todayWeather"
        :src="weatherImg"
        alt="weather
      image"
      />
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "Today",
  props: {
    city: String,
    todayWeather: String,
    todayTemp: Number,
    latitude: Number,
    longitude: Number
  },
  computed: {
    today() {
      return moment().format("dddd DD MMMM");
    },
    weatherImg() {
      /*var weatherNow = this.todayWeather.map(v => v.toLowerCase()); */
      var weatherNow = this.todayWeather.toLowerCase();

      return require(`../assets/${weatherNow}.png`);
    }
  }
};
</script>

<style lang="scss" scoped>
#today {
  height: 45vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  h1 {
    display: flex;
  }
  img {
    margin-top: 1em;
  }
  #temp {
    font-size: 30px;
  }
}
</style>
