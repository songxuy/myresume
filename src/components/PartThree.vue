<template>
  <div :class="partThree" id="part-three"></div>
</template>

<script>

// 引入基本模板
let echarts = require("echarts/lib/echarts");

export default {
  name: "partThree",
  data() {
    return {
      partThree: "part-three",
      curWidth: 0
    };
  },
  beforeMount() {
    this.curWidth = document.documentElement.clientWidth || document.body.clientWidth;
    if(this.curWidth < 1600) {
      this.partThree = "part-three-responsive"
    }
  },
  mounted() {
    this.drawECharts();
  },
  methods: {
    drawECharts() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = echarts.init(document.getElementById("part-three"));

      myChart.setOption({
        // 标题
        title: {
          // 标题文本
          text: "技能分布图",
          // 标题样式
          textStyle: {
            color: "#fff"
          },
          // 标题位置
          x: "center"
        },
        // 移动显示
        tooltip: {
          trigger: "item",
          // 显示文字样式
          formatter: "{a} <br/>{b} : {d}%"
        },
        // 注记
        legend: {
          x: "center",
          y: "bottom",
          textStyle: {
            color: "#fff"
          },
          data: [ "HTML5", "CSS3", "JavaScript", "Canvas", "Vue", "React", "TS", "Other"]
        },
        // 注记显示手柄
        calculable: true,
        // 图形系列
        series: [
          {
            name: "技能分布",
            type: "pie",
            radius: [30, 110],
            roseType: "area",
            data: [
              { value: 20, name: "HTML5" },
              { value: 20, name: "CSS3" },
              { value: 25, name: "JavaScript" },
              { value: 20, name: "Canvas" },
              { value: 30, name: "Vue" },
              { value: 20, name: "React" },
              { value: 20, name: "TS" },
              { value: 20, name: "Other" }
            ]
          }
        ],
        // 颜色调整
        color: ['#00bfff', '#00ffdd', '#207ffc', '#00aeff', "#00eeff", "#006eff", "#0099ff", "#0066ff"]
      });
    }
  }
};
</script>

<style scoped>
.part-three {
  width: 100%;
  height: 500px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  opacity: 0.8;
  background: #18202d;
}
.part-three-responsive {
  width: 100%;
  height: 500px;
  border: 10px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  opacity: 0.8;
  background: #18202d;
}
</style>
