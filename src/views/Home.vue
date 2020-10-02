<template>
  <div class="home">
    <Today
      :city="city"
      :todayTemp="todayTemp"
      :todayWeather="todayWeather"
      :latitude="latitude"
      :longitude="longitude"
    />
    <Forecast :temperature="temperature" />
  </div>
</template>

<script>
// @ is an alias to /src
import Forecast from "@/components/Forecast.vue";
import Today from "@/components/Today.vue";

export default {
  name: "Home",
  components: {
    Forecast,
    Today
  },
  data: () => ({
    city: "",
    todayTemp: 0,
    temperature: [],
    latitude: 0,
    longitude: 0,
    todayWeather: "",
    weather: []
  }),
  methods: {
    getPosition() {
      var options = {
        enableHighAccuracy: true,
        timeout: 5000,
        maximumAge: 0
      };

      var success = pos => {
        var crd = pos.coords;
        this.latitude = crd.latitude;
        this.longitude = crd.longitude;
        this.fetchData();
      };
      function error(err) {
        console.warn(`ERROR (${err.code}): ${err.message}`);
      }

      navigator.geolocation.getCurrentPosition(success, error, options);
    },
    fetchData() {
      fetch(
        `https://api.openweathermap.org/data/2.5/forecast?lat=${this.latitude}&lon=${this.longitude}&appid=${process.env.VUE_APP_OPEN_WEATHER_API}&units=metric`
      )
        .then(response => response.json())
        .then(data => {
          this.temperature = [
            Math.round(data.list[1].main.temp_max),
            Math.round(data.list[2].main.temp_max),
            Math.round(data.list[3].main.temp_max)
          ];
          this.todayTemp = Math.round(data.list[0].main.temp_max);
          this.city = data.city.name;
          this.latitude = data.latitude;
          this.longitude = data.longitude;
          this.todayWeather = data.list[0].weather[0].main;
          this.weather = [
            data.list[1].weather[0].main,
            data.list[2].weather[0].main,
            data.list[3].weather[0].main
          ];
          console.log(data);
        });
    }
  },
  created() {
    this.getPosition();
  }
};
</script>
