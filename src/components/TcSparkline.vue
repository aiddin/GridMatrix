<template>
  <div style="width:250px; height:180px">
    <Sparkline
      @click="togglegradient"
      :transitions="false"
      :seriesColors="seriesColors"
      :data-items="sparklineData"
      :type="types"
    />
    <br />
  </div>
</template>

<script>
import { Sparkline } from "@progress/kendo-vue-charts";
import "@progress/kendo-theme-default/dist/all.css";
export default {
  components: {
    Sparkline,
  },
  props: ["sparklineData"],
  data: function () {
    return {
      seriesColors: ["red"],
      area: "true",
      types: "area",
    };
  },
  methods: {
    togglegradient() {
      this.area = !this.area;
      if (this.area == true) {
        this.types = "area";
      } else {
        this.types = "line";
      }
    },
  },
};
</script>

<style>
.k-sparkline {
  height: 100%;
  width: 100%;
}
</style>
