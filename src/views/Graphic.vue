<template>
  <div class="graphics">
    <h1>Graphic page</h1>
    <canvas id="temperatures" width="400" height="400"></canvas>
  </div>
</template>

<script>
import Chart from "chart.js";
export default {
  data: () => ({
    temp: [3, -8, 15, 5]
  }),
  props: {},
  mounted() {
    this.temperatureLine();
  },
  methods: {
    temperatureLine() {
      const tempData = document.getElementById("temperatures").getContext("2d");

      // eslint-disable-next-line no-unused-vars
      const temperature = new Chart(tempData, {
        type: "line",
        data: {
          labels: ["Monday", "Tuesday", "Wednesday", "Thursday"],
          datasets: [
            {
              label: "temperature",
              data: this.temp,
              order: 0,
              borderColor: "rgba( 255, 255, 255)"
            }
          ]
        },
        options: {
          title: {
            display: true,
            text: "Temperature by day",
            fontColor: "#fff"
          },
          legend: {
            labels: {
              fontColor: "#fff"
            }
          },
          scales: {
            yAxes: [
              {
                ticks: {
                  min: -15,
                  max: 40
                }
              }
            ]
          }
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.graphics {
  height: 85vh;
  h1 {
    display: flex;
    justify-content: center;
  }
}
</style>
