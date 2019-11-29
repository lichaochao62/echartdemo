<template>
  <div>
    <h1>{{content.title}}</h1>
    <el-tabs
      type="border-card "
      v-model="menuactive"
      v-if="content.menu.length >=1"
      @tab-click="handleClick"
    >
      <el-tab-pane :label="item" :name="item" v-for="(item,index) in content.menu" :key="index"></el-tab-pane>
    </el-tabs>
    <div v-show="showtable">
      <div :id="echartid" ref="echartdiv" style="width:500px;height:400px"></div>
    </div>
    <div v-show="showtable">
      <template v-if=" actdata &&  actdata.tabledata  && actdata.tabledata.data.length>0 ">
        <el-table :data="actdata.tabledata.data">
          <template v-for="(item,index) in actdata.tabledata.lables">
            <el-table-column :key="index" :prop="item.prop" :label="item.label"></el-table-column>
          </template>
        </el-table>
      </template>
    </div>
    <el-button type="primary" @click="changed()">切换</el-button>
  </div>
</template>
<script>
import echart from "echarts";
export default {
  data() {
    return {
      actdata: {
        echart: [],
        tabledata: { lables: [], data: [] }
      },
      menuactive: "",
      actNames: [],

      myChart: {},
      echartid: ""
    };
  },
  watch: {
    content: {
      handler(val) {
        console.log(val);
        this.menuactive = val.menu[0];
        this.actdata = val.data[0];
        this.chengedecharts(this.actdata);
      },
      deep: true
    }
  },
  computed: {},
  props: {
    showtable: {
      type: Boolean,
      default: false
    },
    title: {
      type: String,
      default: ""
    },
    content: {
      type: Object,
      default: () => {
        return {
          title: "",
          menu: [],
          data: { echart: "", tabledata: { lables: [], data: [] } }
        };
      }
    }
  },
  mounted() {
    this.actdata = this.content.data[0];
    this.echartid = "t" + Math.random();

    this.chengedecharts(this.actdata);
  },
  methods: {
    changed() {
      this.showtable = !this.showtable;
    },
    handleClick(tab) {
      this.actdata = this.content.data[tab.index];
      this.echartid = "t" + Math.random();
      this.chengedecharts(this.actdata);
    },
    chengedecharts(actdata) {
      this.actNames = [];
      
      actdata.echart.forEach(element => {
        if (element.type == "bar") {
          element.barWidth = "10";
        }
        this.actNames.push(element.name);
      });
      let option = {
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "cross",
            crossStyle: {
              color: "#999"
            }
          }
        },
        toolbox: {
          feature: {
            dataView: { show: true, readOnly: false },
            magicType: { show: true, type: ["line", "bar"] },
            restore: { show: true },
            saveAsImage: { show: true }
          }
        },
        legend: {
          data: []
        },
        xAxis: [
          {
            type: "category",
            data: [
              "1月",
              "1月",
              "1月",
              "1月",
              "1月",
              "1月",
              "1月",
              "1月",
              "1月",
              "1月",
              "1月",
              "1月"
            ],
            axisPointer: {
              type: "shadow"
            }
          }
        ],
        yAxis: [
          {
            type: "value",
            name: "水量",
            min: 0,
            max: 250,
            interval: 50,
            axisLabel: {
              formatter: "{value} ml"
            }
          }
        ],
        series: []
      };

      option.legend.data = this.actNames;
      if (actdata.echart.length > 0) {
        option.series = actdata.echart;
      } else {
        option.series = [];
      }

      if (this.myChart) {
        this.myChart = echart.init(this.$refs.echartdiv);
      }
      this.myChart.setOption(option);

      // 绘制图表
      console.log(actdata);
      console.log(option);
    }
  }
};
</script>