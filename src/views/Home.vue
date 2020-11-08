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
      const options = {
        enableHighAccuracy: true,
        timeout: 5000,
        maximumAge: 0
      };

      const success = pos => {
        const crd = pos.coords;
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
              day: data.list[3].dt_txt,
              condition: data.list[11].weather[0].main,
              temperature: Math.round(data.list[9].main.temp_max)
            },
            {
              day: data.list[11].dt_txt,
              condition: data.list[19].weather[0].main,
              temperature: Math.round(data.list[17].main.temp_max)
            },
            {
              day: data.list[19].dt_txt,
              condition: data.list[27].weather[0].main,
              temperature: Math.round(data.list[27].main.temp_max)
            }
          ];
        });
    }
  },
  created() {
    this.getPosition();
  }
};
</script>
