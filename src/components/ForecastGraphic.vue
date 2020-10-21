<template>
  <div class="graphics">
    <canvas id="temperatures" width="400" height="400"></canvas>
  </div>
</template>

<script>
import Chart from "chart.js";
import dayjs from "dayjs";

export default {
  name: "ForecastGraphic",
  props: {
    weathers: Array,
    days: Array
  },
  methods: {
    temperatureLine() {
      const tempData = document.getElementById("temperatures").getContext("2d");
      // eslint-disable-next-line no-unused-vars
      const temperatures = new Chart(tempData, {
        type: "line",
        data: {
          labels: [
            dayjs(this.days[0]).format("dddd"),
            dayjs(this.days[1]).format("dddd"),
            dayjs(this.days[2]).format("dddd")
          ],
          datasets: [
            {
              label: "temperature by day",
              data: this.weathers,
              order: 0,
              backgroundColor: "rgba(50, 115, 220, 0.1)",
              borderColor: "rgba( 255, 255, 255)"
            }
          ]
        },
        options: {
          title: {
            display: true,
            text: "Forecast temperatures",
            fontColor: "#fff",
            fontSize: 20
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
                  max: 40,
                  callback: function(value) {
                    return value + "°c";
                  },
                  fontColor: "#fff"
                }
              }
            ],
            xAxes: [
              {
                ticks: {
                  fontColor: "#fff"
                }
              }
            ]
          }
        }
      });
    }
  },
  mounted() {
    this.temperatureLine();
  }
};
</script>

<style lang="scss" scoped>
.graphics {
  height: 95vh;
  h1 {
    display: flex;
    justify-content: center;
  }
}
</style>
