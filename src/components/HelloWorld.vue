<template>
  <div>
    <el-tabs type="border-card " @tab-click="handleMainClick">
      <el-tab-pane :label="sub.title" v-for="(sub,subindex) in pagedata" :key="subindex"></el-tab-pane>
    </el-tabs>
    <el-tabs type="border-card " v-if="actsubdata.isshow" @tab-click="handleSubClick">
      <el-tab-pane :label="item.title" v-for="(item,index) in actsubdata.contents" :key="index"></el-tab-pane>
    </el-tabs>
    <DataView :showtable="true" v-for="(item,index) in details"  :key="index" :content="item"></DataView>
  </div>
</template>

<script>
import DataView from "@/components/DataView.vue";

export default {
  name: "HelloWorld",
  components: {
    DataView
  },
  props: {},
  data() {
    return {
      pagedata: [{
          title: "空调",
          children: {
            isshow: true,
            contents: [
              { title: "App控制",children: { isshow: true, contents: [{title:'效率1',menu:['功率1','功率2','功率3'],data:[{echart:'功率1echart',table:'功率1-table'},{echart:'功率2echart',table:'功率2-table'},{echart:'功率3echart',table:'功率3-table'}]},
                                                                        {title:'效率2',menu:[],data:[{echart:'echart',table:'table'}]},
                                                                        {title:'效率3',menu:[],data:[{echart:'echart',table:'table'}]}
                                                                        ] } },
              { title: "大屏控制", children: { isshow: true, contents: [{title:'效率2',menu:[],data:[{echart:'echart',table:'table'}]}] } },
              { title: "音响控制", children: { isshow: true, contents: [{title:'效率2',menu:[],data:[{echart:'echart',table:'table'}]}] } }
            ]
          }
        },
        {
          title: "洗衣机",
          children: {
            isshow: true,
            contents: [
              {
                title: "品牌",
                children: {isshow: true,
                  contents: [{title:'效率2',menu:[],data:[{echart:'echart',table:'table'}]},
                  {title:'效率2',menu:[],data:[{echart:'echart',table:'table'}]},
                  {title:'效率2',menu:[],data:[{echart:'echart',table:'table'}]}
                ]}
              },
              {
                title: "产地",
                children: {
                  isshow: true,
                  contents: [{
                      title: "吉林省",children: { isshow: true, contents: [{title:'效率2',menu:[],data:[{echart:'echart',table:'table'}]}] }
                    }]
                }
              }
            ]
          }
        },
        {
          title: "冰箱",
          children: {
            isshow: false,
            contents: [
              {
                title: "a",
                children: {
                  isshow: true,
                  contents: [
                    {
                      title: "吉林省",
                      children: { isshow: true, contents: [] }
                    }
                  ]
                }
              }
            ]
          }
        }
      ],
      actsubdata: {},
      details: []
    };
  },
  mounted() {
    this.actsubdata = this.pagedata[0].children;
    this.details = this.actsubdata.contents[0].children.contents;
    console.log(this.details);
    console.log("hello");
  },
  methods: {
    //第一层tab切换
    handleMainClick(tab, event) {
      this.actsubdata = this.pagedata[tab.index].children;
      console.log(this.actsubdata);
      this.details = this.actsubdata.contents[0].children.contents;
      console.log(tab, event);
    },
    //第二层tab切换
    handleSubClick(tab) {
      console.log(tab.index)
      console.log(this.actsubdata);
      this.details = this.actsubdata.contents[tab.index].children.contents; 
       console.log(this.details);
    }
  }
};
</script>

