<template>
  <ForecastGraphic :weathers="weathers" :days="days" />
</template>

<script>
import ForecastGraphic from "@/components/ForecastGraphic.vue";

export default {
  name: "Graphic",
  components: {
    ForecastGraphic
  },
  data: () => ({
    latitude: 0,
    longitude: 0,
    weathers: [],
    days: []
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
          this.weathers = [
            Math.round(data.list[9].main.temp_max),
            Math.round(data.list[17].main.temp_max),
            Math.round(data.list[27].main.temp_max)
          ];
          this.days = [
            /*    {
              daylabel: data.list[3].dt_txt
            },
            {
              daylabel: data.list[11].dt_txt
            },
            {
              daylabel: data.list[19].dt_txt
            } */
            data.list[3].dt_txt,
            data.list[11].dt_txt,
            data.list[19].dt_txt
          ];
          console.log(this.weathers);
        });
    }
  },
  created() {
    this.getPosition();
  }
};
</script>
