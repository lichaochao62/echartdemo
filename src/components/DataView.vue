<template>
    <div>
        <h1>{{content.title}}</h1>
        <el-tabs type="border-card " v-if="content.menu.length >=1" @tab-click="handleClick">
      <el-tab-pane :label="item" v-for="(item,index) in content.menu" :key="index"></el-tab-pane>
    </el-tabs>
        <div v-show="showtable"><h1>{{actdata.echart}}</h1></div>
        <div v-show="!showtable"><h1>{{actdata.table}}</h1></div>
        <el-button type="primary" @click="changed()">切换</el-button>
    </div>
</template>
<script>
    export default {
      data() {
        return {  
            actdata:{
                echart:'',table:''
            }        
        }
      },
      props:{
          showtable:{
              type:Boolean,
              default:false,
          },
          title:{
              type:String,
              default:''
          },
          content:{
              type:Object,
              default:()=>{
                  return {
                      title:'',
                      menu:[],
                      data:{echart:'',table:''}
                  }
              }
          }
      },
      mounted(){
        this.actdata = this.content.data[0];
        console.log(this.content)
      },
      methods:{
          changed()
          {
              this.showtable=!this.showtable
          },
          handleClick(tab)
          {
              this.actdata = this.content.data[tab.index];
          }
      }
    }
  </script>