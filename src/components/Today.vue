<template>
  <div id="today">
    <div>
      <h1>{{ today }}</h1>
    </div>
    <div id="temp">{{ temperature }}°c {{ name }}</div>
    <img src="../assets/sun.png" alt="cloudy weather" />
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "Today",
  data: () => ({
    name: "",
    sys: { country: "" },
    temperature: 27
  }),
  created() {
    fetch(
      "http://api.openweathermap.org/data/2.5/weather?q=Houilles&appid=374f5dd6b4f601b323b685f32da6028c&units=metric"
    )
      .then(response => response.json())
      .then(data => {
        this.temperature = data.main.temp_max;
        this.name = data.name;
        this.sys = data.sys.country;
        console.log(data);
      });
  },
  computed: {
    today() {
      return moment().format("dddd");
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
    font-size: 25px;
  }
}
</style>
