<template>
  <div class="home">
    <Today
      :city="city"
      :todayTemp="todayTemp"
      :todayWeather="todayWeather"
      :latitude="latitude"
      :longitude="longitude"
    />
    <Forecast :weathers="weathers" />
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
    latitude: 0,
    longitude: 0,
    todayWeather: "",
    weathers: []
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
          this.todayTemp = Math.round(data.list[0].main.temp_max);
          this.city = data.city.name;
          this.latitude = data.latitude;
          this.longitude = data.longitude;
          this.todayWeather = data.list[0].weather[0].main;
          this.weathers = [
            {
              condition: data.list[1].weather[0].main,
              temperature: Math.round(data.list[1].main.temp_max)
            },
            {
              condition: data.list[2].weather[0].main,
              temperature: Math.round(data.list[2].main.temp_max)
            },
            {
              condition: data.list[3].weather[0].main,
              temperature: Math.round(data.list[3].main.temp_max)
            }
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
