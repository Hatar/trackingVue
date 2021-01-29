<template>
  <div class="container">
    <Doses :Total="totalVac" :totalReported="totalReported" :totalDoses="totalDoses" :perThousand="perThousand"/>
    <Vaccination :socket="Socket"/>
    <Province :provinces="provinces"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Doses from "./../components/Doses.vue";
import Vaccination from "./../components/Vaccination.vue";
import Province from "./../components/Province.vue";
//import axios from "axios";
import io from 'socket.io-client/dist/socket.io';

export default {
  name: "Home",
  components: {
    Doses,
    Vaccination,
    Province
  },
  data() {
    return {
      provinces: null,
      totalVac:null,
      totalDoses:null,
      totalReported:null,
      totalEstimade:null,
      perThousand:'',
      Socket : io.connect("localhost:8000")
    };
  },
  created() {
    this.getProvince();
  },
  methods: {
    getProvince() {
      this.Socket.on("data", (data) => {
        //console.log(data)
          this.provinces = data.data.data
          this.totalVac   = data.data.data.map(item => parseInt(item.doses)).reduce((y, z) => y + z) 
          this.totalReported   = data.data.data.map(item => parseInt(item.Reported)).reduce((y, z) => y + z)
          this.totalDoses   = data.data.reported_doses.reduce((a,b) => a+b)
          this.perThousand = this.totalDoses / 100
      });
     /* axios
        .get("http://localhost:3000/data")
        .then(res => {
            console.log(res.data.data)
            this.provinces = res.data.data;
            this.totalVac =res.data.data.map(item => parseInt(item.doses)).reduce((y, z) => y + z)
        })
        .catch(err => (this.provinces = err.data));*/
    }
  }
};
</script>
