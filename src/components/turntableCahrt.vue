<template>
  <div class="turnTable">
    <v-chart class="chart" :option="option" />
    <el-button @click="startRotate">{{ desText }}</el-button>
  </div>
</template>

<script>
import { use } from "echarts/core";
import { CanvasRenderer } from "echarts/renderers";
import { PieChart } from "echarts/charts";
import { LegendComponent } from "echarts/components";
import VChart, { THEME_KEY } from "vue-echarts";

use([CanvasRenderer, PieChart, LegendComponent]);

export default {
  name: "HelloWorld",
  components: {
    VChart,
  },
  provide: {
    [THEME_KEY]: "light",
  },
  data() {
    return {
      hasStartRotate: false,
      desText: "开始",
      timer: null,
      speed: 5,
      maxSpeed: 20,
      option: {
        animation: false,
        legend: {
          orient: "horizontal",
          left: "center",
          top: "top",
          selectedMode: false,
          data: ["逛盒马", "看电影", "逛山姆", "小礼物"],
        },
        series: [
          {
            name: "TurnTable",
            startAngle: 0,
            type: "pie",
            radius: "80%",
            center: ["50%", "50%"],
            data: [
              { value: 10, name: "逛盒马" },
              { value: 20, name: "看电影" },
              { value: 30, name: "逛山姆" },
              { value: 20, name: "小礼物" },
            ],
            emphasis: {
              scale: false,
            },
            label: {
              show: false,
            },
          },
        ],
      },
    };
  },
  methods: {
    startRotate() {
      if (!this.hasStartRotate) {
        this.hasStartRotate = true;
        this.desText = "停止";
        this.timer = setInterval(() => {
          if (this.speed < this.maxSpeed) this.speed += 0.1;
          this.option.series[0].startAngle += this.speed;
        }, 20);
      } else {
        const rdm = Math.random() * 1000;
        setTimeout(() => {
          this.hasStartRotate = false;
          this.desText = "开始";
          clearInterval(this.timer);
        }, rdm);
      }
    },
  },
};
</script>

<style scoped>
.chart {
  height: 400px;
}
.turnTable {
}
</style>