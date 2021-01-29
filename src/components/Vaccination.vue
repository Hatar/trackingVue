<template>
  <div class="chart-container">
    <canvas ref="my-canvas"></canvas>
  </div>
</template>
<script>
//import axios from "axios";
import Chart from 'chart.js';

export default {
  props:['socket'],
  data(){
    return {
        user: '',
        message: ''
    }
  },
  mounted() {
    this.initChart() 
  },
  created() {
    this.setupConnection()
  },
  methods: {
    setupConnection() {        
        this.socket.on('connect',() =>{
            console.log("connected");
            this.socket.emit('join','serial22');
        })
        
    },
    initChart() {
      this.socket.on("data", (data) => {
        console.log(data)
        var ctx = this.$refs["my-canvas"].getContext("2d");
        new Chart(ctx, {
            type: "bar",
            data: {
              labels: data.data.labels.map((label) => label),
              datasets: [
                {
                  label: "Reported Doses",
                  type: "bar",
                  data: data.data.reported_doses.map((resport) => resport),
                  backgroundColor: "rgba(75, 192, 192, 0.2)",
                  borderColor: "rgba(75, 192, 192, 1)",
                  borderWidth: 1,
                  yAxisID: "A",
                },
                {
                  label: "Estimated Doses*",
                  type: "bar",
                  data: data.data.estimated_doses.map((estimated_doses) => estimated_doses),
                  backgroundColor: "rgba(54, 162, 235, 0.2)",
                  borderColor: "rgba(54, 162, 235, 1)",
                  borderWidth: 1,
                  yAxisID: "A",
                },
                {
                  label: "Daily Doses",
                  type: "line",
                  data: data.data.daily_doses.map((daily_doses) => daily_doses),
                  borderColor: "rgba(255, 99, 132, 1)",
                  borderWidth: 1,
                  yAxisID: "B",
                },
              ],
            },
            options: {
              responsive: true,
              maintainAspectRatio: false,
              title: {
                display: true,
                text: "Daily Trend for last 30 days",
                fontColor: "#bbb",
              },
              legend: {
                display: true,
                position: "bottom",
                labels: {
                  fontColor: "#bbb",
                },
              },
              scales: {
                yAxes: [
                  {
                    id: "A",
                    position: "left",
                    stacked: true,
                    ticks: {
                      beginAtZero: true,
                      callback: (label) => +label / 1000000 + "M",
                    },
                  },
                  {
                    id: "B",
                    position: "right",
                    ticks: {
                      beginAtZero: true,
                      callback: (label) => +label / 1000000 + "M",
                    },
                    gridLines: {
                      display: false,
                    },
                  },
                ],
                xAxes: [
                  {
                    stacked: true,
                    ticks: {
                      min: "27 Dec 2020",
                    },
                  },
                ],
              },
              plugins: {
                zoom: {
                  pan: {
                    enabled: false,
                    mode: "x",
                  },
                  zoom: {
                    enabled: false,
                    mode: "x",
                  },
                },
              },
            },
          })
      });
    },
  },
};
</script>

<style scoped>
.chart-container {
  width: 100%;
  height: 600px;
}
</style>
