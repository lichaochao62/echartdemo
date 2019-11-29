<template>
  <div>
    <!-- <el-tabs type="border-card " @tab-click="handleMainClick">
      <el-tab-pane :label="sub.title" v-for="(sub,subindex) in pagedata" :key="subindex"></el-tab-pane>
    </el-tabs> -->
    <button @click="kongtiaochenged">空调</button>
    <button @click="xiyijichenged">洗衣机</button>
    <button @click="bingxiangchenged">冰箱</button>
    <el-tabs type="border-card " v-if="actsubdata.isshow" @tab-click="handleSubClick">
      <el-tab-pane :label="item.title" v-for="(item,index) in actsubdata.contents" :key="index"></el-tab-pane>
    </el-tabs>

    <DataView :showtable="true" v-for="(item,index) in details" :key="index" :content.sync="item"></DataView>
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
      pagedata: [
        {
          title: "空调",
          children: {
            isshow: true,
            contents: [
              {
                title: "App控制",
                children: {
                  isshow: true,
                  contents: [
                    {
                      title: "效率1",
                      menu: ["功率1", "功率2", "功率3"],
                      data: [
                        { echart: [ {
                                  name:'蒸发量',
                                  type:'bar',
                                  data:[2.0, 4.9, 7.0, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20.0, 6.4, 3.3],
                                  barWidth:'30'
                              },
                              {
                                  name:'降水量',
                                  type:'bar',
                                  data:[2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3],
                                  barWidth:'30'
                              },
                              {
                                  name:'平均温度',
                                  type:'line',
                                  data:[2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2]
                              }], 
                            tabledata: {
                                  lables: [
                                    { label: "用户ID", prop: "uid" },
                                    { label: "名称", prop: "cname" },
                                    { label: "性别", prop: "sex" }
                            ],
                            data: [
                              { uid: 1, cname: "生命一号", sex: "瓶装" },
                              { uid: 2, cname: "生命二号", sex: "瓶装" },
                              { uid: 3, cname: "生命三号", sex: "片装" }
                            ]
                          } },
                        { echart: [ {
                                  name:'排水量',
                                  type:'bar',
                                  data:[112.0, 41.9, 7.0, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20.0, 6.4, 3.3],
                                  barWidth:'30'
                              },
                              {
                                  name:'污水量',
                                  type:'bar',
                                  data:[112.6, 51.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3],
                                  barWidth:'30'
                              },
                              {
                                  name:'平均量',
                                  type:'line',
                                  data:[12.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2]
                              }], tabledata: {
                            lables: [
                              { label: "班级", prop: "id" },
                              { label: "学生", prop: "stuents" },
                              { label: "老师", prop: "teacher" }
                            ],
                            data: [
                              { id: 1, stuents: 50, teacher: "李老师" },
                              { id: 5, stuents: 55, teacher: "杨老师" },
                              { id: 3, stuents: 60, teacher: "孙老师" }
                            ]
                          } },
                        { echart: [], tabledata: {
                            lables: [
                              { label: "年级", prop: "id" },
                              { label: "班数", prop: "classes" },
                              { label: "教导主任", prop: "teacher" }
                            ],
                            data: [
                              { id: 1, classes: 10, teacher: "王主任" },
                              { id: 2, classes: 12, teacher: "陈主任" },
                              { id: 3, classes: 1, teacher: "副校长" }
                            ]
                          }  }
                      ]
                    },
                    {
                      title: "效率2",
                      menu: [],
                      data: [{ echart: [], tabledata: {
                            lables: [
                              { label: "商品ID3", prop: "id" },
                              { label: "商品名称3", prop: "name" },
                              { label: "类型3", prop: "specs" }
                            ],
                            data: [
                              { id: 1, name: "生命一号3", specs: "瓶装" },
                              { id: 2, name: "生命二号3", specs: "瓶装" },
                              { id: 3, name: "生命三号3", specs: "片装" }
                            ]
                          } }]
                    },
                    {
                      title: "效率3",
                      menu: [],
                      data: [{ echart: [], tabledata: {
                            lables: [
                              { label: "商品ID4", prop: "id" },
                              { label: "商品名称4", prop: "name" },
                              { label: "类型4", prop: "specs" }
                            ],
                            data: [
                              { id: 1, name: "生命一号4", specs: "瓶装" },
                              { id: 2, name: "生命二号4", specs: "瓶装" },
                              { id: 3, name: "生命三号4", specs: "片装" }
                            ]
                          } }]
                    }
                  ]
                }
              },
              {
                title: "大屏控制",
                children: {
                  isshow: true,
                  contents: [
                    {
                      title: "效率2",
                      menu: [],
                      data: [{echart: [],tabledata: {
                            lables: [
                              { label: "商品ID", prop: "id" },
                              { label: "商品名称", prop: "name" },
                              { label: "类型", prop: "specs" }
                            ],
                            data: [
                              { id: 1, name: "生命一号5", specs: "瓶装" },
                              { id: 2, name: "生命二号5", specs: "瓶装" },
                              { id: 3, name: "生命三号5", specs: "片装" }
                            ]
                          }
                        }
                      ]
                    }
                  ]
                }
              },
              {
                title: "音响控制",
                children: {
                  isshow: true,
                  contents: [
                    {
                      title: "效率2",
                      menu: [],
                      data: [{ echart: [], tabledata: {
                            lables: [
                              { label: "商品1ID", prop: "id" },
                              { label: "商品1名称", prop: "name" },
                              { label: "类型1", prop: "specs" }
                            ],
                            data: [
                              { id: 1, name: "生命1一号6", specs: "瓶装" },
                              { id: 2, name: "生命1二号6", specs: "瓶装" },
                              { id: 3, name: "生命1三号6", specs: "片装" }
                            ]
                          } }]
                    }
                  ]
                }
              }
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
                children: {
                  isshow: true,
                  contents: [
                    {
                      title: "效率2",
                      menu: [],
                      data: [{},
                          { echart: [], tabledata: {
                            lables: [
                              { label: "海信洗衣机ID", prop: "id" },
                              { label: "海信商品名称", prop: "name" },
                              { label: "海信类型", prop: "specs" }
                            ],
                            data: [
                              { id: 1, name: "海信洗衣机1", specs: "瓶装" },
                              { id: 2, name: "海信洗衣机2", specs: "瓶装" },
                              { id: 3, name: "海信洗衣机3", specs: "片装" }
                            ]
                          } }
                          ]
                    },
                    {
                      title: "效率2",
                      menu: ['海尔1','海信1'],
                      data: [{ echart: [], tabledata: {
                            lables: [
                              { label: "海尔1商品ID", prop: "id" },
                              { label: "海尔1洗衣机名称", prop: "name" },
                              { label: "海尔1类型", prop: "specs" }
                            ],
                            data: [
                              { id: 1, name: "海尔1洗衣机4", specs: "瓶装" },
                              { id: 2, name: "海尔1洗衣机7", specs: "瓶装" },
                              { id: 3, name: "海尔1洗衣机6", specs: "片装" }
                            ]
                          } },
                          { echart: [], tabledata: {
                            lables: [
                              { label: "海信1商品ID", prop: "id" },
                              { label: "海信1洗衣机名称", prop: "name" },
                              { label: "海信1类型", prop: "specs" }
                            ],
                            data: [
                              { id: 1, name: "海信1洗衣机4", specs: "瓶装" },
                              { id: 2, name: "海信1洗衣机7", specs: "瓶装" },
                              { id: 3, name: "海信1洗衣机6", specs: "片装" }
                            ]
                          } }]
                    },
                    {
                      title: "效率2",
                      menu: [],
                      data: [{ echart:[], tabledata: {
                            lables: [
                              { label: "商品ID", prop: "id" },
                              { label: "商品名称", prop: "name" },
                              { label: "洗衣机", prop: "specs" }
                            ],
                            data: [
                              { id: 1, name: "洗衣机8", specs: "瓶装" },
                              { id: 2, name: "洗衣机9", specs: "瓶装" },
                              { id: 3, name: "洗衣机10", specs: "片装" }
                            ]
                          } }]
                    }
                  ]
                }
              },
              {
                title: "产地",
                children: {
                  isshow: true,
                  contents: [
                    {
                      title: "吉林省",
                      children: {
                        isshow: true,
                        contents: [
                          {
                            title: "效率2",
                            menu: [],
                            data: [{ echart: "echart", table: "table" }]
                          }
                        ]
                      }
                    }
                  ]
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
    console.log("hello");
  },
  methods: {
    //第一层tab切换
    // handleMainClick(tab, event) {
    //   this.actsubdata = this.pagedata[tab.index].children;
    //   this.details = this.actsubdata.contents[0].children.contents;
    // },
    //第二层tab切换
    handleSubClick(tab) {
      this.details = JSON.parse(JSON.stringify(this.actsubdata.contents[tab.index].children.contents));
    },
    kongtiaochenged()
    {
      
    },
    xiyijichenged(){

    },
    bingxiangchenged(){

    } 
  }
};
</script>

