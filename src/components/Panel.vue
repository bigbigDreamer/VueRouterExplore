<template>
  <div>
    <el-col :span="14" :offset="5">
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>热帖榜</span>
        </div>
        <div class="text item">
          <ul>
            <li v-for="(item,index) in Persons" :key="index" @click="handleClick(index)" ref="li">
              {{item.content}}
            </li>
          </ul>
        </div>
      </el-card>
    </el-col>
  </div>
</template>

<script>
  export default {
    name: "Panel",
    data(){
      return {
        Persons:[]
      }
    },
    methods: {
      handleClick(index) {
        this.$router.push({ name: 'single',params: { userId: index }})
        this.$pub.publish('d',{content:this.$refs.li[index].innerText,topic:this.Persons[index].topic})
      }
    },
    mounted(){
      this.$pub.subscribe('person',(msg,data)=>{
        console.log(123)
        this.Persons = data
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
