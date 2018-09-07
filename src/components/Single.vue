<template>
      <div>
        <el-col :span="14" :offset="5">
          <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>{{this.topic}}</span>
      </div>
      <div class="text item">
        <ul>
          <li>
            {{this.content1}}
          </li>
        </ul>
      </div>
          </el-card>
        </el-col>
      </div>
</template>

<script>
    export default {
       name: "Single",
       data(){
          return {
            content1:'',
            topic:''
          }
       },
     created(){//此处只是测试一下而已，我的猜测以及常规套路是正确的
        // console.log('6446464')
        this.$pub.subscribe('d',(msg,content)=>{
         //console.log('bug通过了')
        //console.log(content)
          this.topic = content.topic;
          this.content1=content.content
        })
      }
    }
</script>

<style scoped>
  .text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 18px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both
  }

  .box-card {
    width: 100%;
    height: 500px;
    background-color: #434343;
    color: #C7C7C7;
    border: none;
  }
</style>
