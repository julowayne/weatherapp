<template>
  <div id="today">
    <div>
      <h1>{{ today }}</h1>
    </div>
    <div id="temp">{{ temperature[0] }}°c {{ city }}</div>
    <div>
      <img
        v-if="weather"
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
    weather: String,
    temperature: Number,
    latitude: Number,
    longitude: Number
  },
  data: () => ({}),
  methods: {},

  computed: {
    today() {
      return moment().format("dddd DD MMMM");
    },
    weatherImg: function() {
      return require(`../assets/${this.weather.toLowerCase()}.png`);
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
