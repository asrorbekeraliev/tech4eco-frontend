<template>
  <div style="background-color: white; ">

    <el-card class="box-card" shadow="always" style="min-height: 800px">
      <el-row style="margin-top: 30px; margin-bottom: 30px">
        <h2 style="color: #114fbe; margin-bottom: 35px">Monitoring of field parameters through<br>Wireless Sensor and Actuator Network Devices </h2>
        <el-col :span="12" v-for = 'node in this.nodes' v-bind:key="node.nodeNumber">
          <el-button type="success" @click = getData(node)>Device №:{{ node }}</el-button>
        </el-col>
      </el-row>

      <div >
        <ccv-line-chart :data='data1' :options='options' v-show="status"></ccv-line-chart>
      </div>
    </el-card>

  </div>
</template>

<script>
import Vue from "vue";

import "@carbon/styles/css/styles.css";

import "@carbon/charts/styles.css";
import chartsVue from "@carbon/charts-vue";

// IBM Plex should either be imported in your project by using Carbon
// or consumed manually through an import
import "../ibm-plex-font.css";
import axios from "axios";

Vue.use(chartsVue);

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Chart",
  components: {},
  data() {
    return {

      data1: [],
      nodeNumber: null,
      status: false,
      nodes: [],
      options: {
        "title": "Parameters",
        "axes": {
          "bottom": {
            "title": " Time",
            "mapsTo": "date",
            "scaleType": "time",

          },
          "left": {
            "mapsTo": "value",
            "title": "Value",
            "scaleType": "linear"
          }
        },

        "experimental": true,
        "zoomBar": {
          "top": {
            "enabled": true
          }
        },
        "color": {
          "scale": {
            "Air Temperature": "#fc0101",
            "Soil moisture": "#00feba",
            "Humidity": "#4cff00",
            "Soil Temperature": "#002aff"
          }
        },
        "curve": "curveMonotoneX",
        "height": "400px",
      },
    };

  },
  methods:{
    getNodes(){
      axios
          .get('api/node/get/NodeNumbers')
          .then(res=>{
            this.nodes = res.data;
          })
    },
    getData(node){
      console.log(node);
      axios
          .get(`api/parameter/data/${node}`)
          .then(res=>{
            console.log(res.data)
            this.data1 = res.data;
            this.status = true;


          })
    }
  },

  created() {
    this.getNodes();

  },

};
</script>
