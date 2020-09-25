<template>
  <div id="today">
    <div>
      <h1>{{ today }}</h1>
    </div>
    <div id="temp">{{ temperature }}°c {{ name }}</div>
    <img
      :src="require(`../assets/${weather.toLowerCase()}.png`)"
      alt="weather image"
    />
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "Today",
  data: () => ({
    name: "",
    sys: { city: "" },
    temperature: 0,
    latitude: "",
    longitude: "",
    weather: ""
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
        `https://api.openweathermap.org/data/2.5/forecast?lat=${this.latitude}&lon=${this.longitude}&appid=${process.env.VUE_APP_OPEN_WEATHER_API}&units=metric`
      )
        .then(response => response.json())
        .then(data => {
          this.temperature = Math.round(data.list[0].main.temp_max);
          this.name = data.name;
          this.sys = data.city.name;
          this.latitude = data.latitude;
          this.longitude = data.longitude;
          this.weather = data.list[1].weather[0].main;
          console.log(data);
        });
    }
  },
  created() {
    this.getPosition();
  },
  computed: {
    today() {
      return moment().format("dddd DD MMMM");
    },
    /*   getWeatherImg() {
      if (!this.weather) {
        return;
      }

      const weather = this.weather.toLowerCase();

      return require(`../assets/${weather}.png`); // the module request
    } */
    getWeatherImg: function() {
      if (this.weather === "") return null;
      else if (this.weather === "Rain") return "rain";
      else if (this.weather === "Thunderstorm") return "thunderstorm";
      else if (this.weather === "Drizzle") return "drizzle";
      else if (this.weather === "Snow") return "snow";
      else if (this.weather === "Atmosphere") return "atmoshpere";
      else if (this.weather === "Clear") return "clear";
      else if (this.weather === "Clouds") return "clouds";

      return "";
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
    &.rain {
      content: url(../assets/rain.png);
    }
    &.thunderstorm {
      content: url(../assets/thunderstorm.png);
    }
    &.drizzle {
      content: url(../assets/rain.png);
    }
    &.snow {
      content: url(../assets/snowflake.png);
    }
    &.atmoshpere {
      content: url(../assets/atmosphere.png);
    }
    &.clear {
      content: url(../assets/sun.png);
    }
    &.clouds {
      content: url(../assets/clouds.png);
    }
  }
  #temp {
    font-size: 25px;
  }
}
</style>
