<template>
  <div></div>
</template>
<script>
import echarts from "echarts";
export default {
  name: "MyChart",
  props: {
    //chart类型
    chartType: {
      type: String,
      default: "bar",
    },
    //请求地址url
    url: {
      type: String,
      default: "/data/echartsData.json",
    },
  },
  data() {
    return {
      echart: null,
    };
  },
  methods: {
    //请求json文件
    findData() {
      this.$axios
        .get(this.url, {})
        .then((response) => {
          let option = response.data;
          let chartData = {
            title: {
              text: this.chartType + "Chart",
            },
            xAxis: { data: option.xData },
            yAxis: {},
            series: [
              {
                name: this.chartType,
                type: this.chartType,
                data: option.yData,
              },
            ],
          };
          this.drawChart(chartData);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    drawChart(chartData) {
      // 基于准备好的dom，初始化echarts实例
      let chart = echarts.init(this.$el);
      // 使用刚指定的配置项和数据显示图表。
      chart.setOption(chartData);
    },
  },
  mounted() {
    this.findData();
  },
};
</script>
