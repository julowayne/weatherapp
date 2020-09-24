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
    temperature: 0,
    latitude: "",
    longitude: ""
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
        /*    console.log("Votre position actuelle est :");
        console.log(`Latitude : ${crd.latitude}`);
        console.log(`Longitude : ${crd.longitude}`);
        console.log(`La précision est de ${crd.accuracy} mètres.`);
        console.log(this); */
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
        `https://api.openweathermap.org/data/2.5/weather?lat=${this.latitude}&lon=${this.longitude}&appid=${process.env.VUE_APP_OPEN_WEATHER_API}&units=metric`
      )
        .then(response => response.json())
        .then(data => {
          this.temperature = data.main.temp_max;
          this.name = data.name;
          this.sys = data.sys.country;
          this.latitude = data.latitude;
          this.longitude = data.longitude;
          console.log(data);
        });
    }
  },
  created() {
    this.getPosition();
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
