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
import dayjs from "dayjs";

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
      return dayjs().format("dddd DD MMMM");
    },
    weatherImg() {
      const weatherNow = this.todayWeather.toLowerCase();

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
