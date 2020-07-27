<template>
  <div class="home">
    <!--    {{ name }} {{ sys.country }} {{ temperature }} -->
    <Today />
    <Forecast />
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
  }
  /*   data: () => ({
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
  } */
};
</script>
