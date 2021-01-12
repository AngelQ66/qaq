<template>
  <div class="about">
    <el-dropdown @command="handleCommand">
      <el-button class="el-dropdown-link">
        下拉菜单<i class="el-icon-arrow-down el-icon--right"></i>
      </el-button>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item command="row">横向</el-dropdown-item>
        <el-dropdown-item command="column">纵向</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
    <div :class="'mycharts ' + chartDirection">
      <my-charts class="chart" chartType="line"></my-charts>
      <my-charts class="chart" chartType="bar"></my-charts>
    </div>
  </div>
</template>
<script>
import MyCharts from "@/components/MyCharts.vue";
export default {
  name: "About",
  components: {
    MyCharts,
  },
  data() {
    return {
      chartDirection: "column",
    };
  },
  methods: {
    handleCommand(command) {
      this.chartDirection = command;
    },
  },
};
</script>
<style scoped>
.chart {
  width: 600px;
  height: 400px;
}
.mycharts {
  display: flex;
  margin-top: 50px;
  width: 100%;
  justify-content: center;
  align-items: center;
}
.row {
  flex-direction: row;
}
.column {
  flex-direction: column;
}
</style>
