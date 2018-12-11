<template>
  <div class="part-two" id="part-two"></div>
</template>

<script>
// 引入基本模板
let echarts = require("echarts/lib/echarts");

// 引用中国地图
require("echarts/map/js/china.js");

export default {
  name: "partTwo",
  data() {
    return {};
  },
  mounted() {
    this.drawECharts();
  },
  methods: {
    drawECharts() {

      // 基于准备好的dom，初始化echarts实例
      let myChart = echarts.init(document.getElementById("part-two"));

      // 排行前五城市
      let myFirendCity = [
        { name: "成都", value: ["104.06", "30.67", "10"] },
        { name: "深圳", value: ["114.07", "22.62", "8"] },
        { name: "杭州", value: ["120.19", "30.26", "8"] },
        { name: "北京", value: ["116.46", "39.92", "8"] },
        { name: "上海", value: ["121.48", "31.22", "6"] },
        /* { name: "成都", value: 10 },
        { name: "深圳", value: 8 },
        { name: "杭州", value: 8 },
        { name: "北京", value: 8 },
        { name: "上海", value: 6 }, */
      ];

      // 好友分布省份
      let myFriendProvince = [
        { name: "山东"},
        { name: "四川"},
        { name: "广东" },
        { name: "广西"},
        { name: "北京" },
        { name: "甘肃"},
        { name: "上海" },
        { name: "陕西"},
        { name: "湖北"},
        { name: "湖南"},
        { name: "山西"},
        { name: "辽宁"},
        { name: "江苏"},
        { name: "河北"},
        { name: "海南"},
        { name: "河南"}
      ];

      myChart.setOption({
        // 标题
        title: {
          text: "期望工作城市Top5",
          textStyle: {
            color: "#fff"
          },
          subtext: "2018年期望",
          subtextStyle: {
            color: "#fff"
          },
          x: "center"
        },
        // 移动显示
        tooltip: {
          trigger: "item",
          // 鼠标移动过去显示
          formatter: function(params) {
            if (params.value[2] == undefined) {
              if(!params.name) {
                return "该地区暂无期望";
              } else {
                return params.name;
              }
            } else {
              return params.name;
            }
          }
        },
        // 左边注记
        /* visualMap: {
          text: ["", "好友数"],
          min: 0,
          max: 30,
          // 是否能通过手柄显示
          calculable: true,
          inRange: {
            color: ["#e4e004", "#ff5506", "#ff0000"]
          },
          textStyle: {
            color: "#fff"
          }
        }, */
        // geo
        geo: {
          map: "china"
        },
        // 数据
        series: [
          // 排行前五城市
          {
            name: "排行前五",
            type: "effectScatter",
            coordinateSystem: "geo",
            symbolSize: function(val) {
              return val[2] * 2;
            },
            showEffectOn: "render",
            rippleEffect: {
              brushType: "stroke"
            },
            hoverAnimation: true,
            label: {
              normal: {
                formatter: "{b}",
                position: "right",
                show: true,
                color: "#fff"
              }
            },
            itemStyle: {
              normal: {
                color: "#ddb926",
                shadowBlur: 10,
                shadowColor: "#333"
              }
            },
            // 类似于 z-index
            zlevel: 1,
            data: myFirendCity,
          },
          // 好友分布省份
          {
            name: "好友数",
            type: "map",
            mapType: "china",
            // 是否允许缩放
            roam: false,
            label: {
              // 显示省份标签
              normal: {
                formatter: myFirendCity,
                show: false,
                textStyle: {
                  color: "#fff"
                }
              },
              // 对应的鼠标悬浮效果
              emphasis: {
                show: false
              }
            },
            itemStyle: {
              normal: {
                borderWidth: 0.5, // 区域边框宽度
                borderColor: "#fff", // 区域边框颜色
                areaColor: "deepskyblue" // 区域颜色
              },
              // 对应的鼠标悬浮效果
              emphasis: {
                borderWidth: 1,
                borderColor: "#fff",
                areaColor: "#00aeff"
              }
            },
            // 数据
            data: myFriendProvince
          }
        ]
      });
    }
  }
};
</script>

<style scoped>
.part-two {
  width: 100%;
  height: 500px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
</style>