<!-- 首页 -->
<template>
  <div :style="{backgroundImage:'url(https://xpoet.cn/images/bg.svg)'}">
    <sg-navbar ></sg-navbar>
    <div class="container">
      <el-row :gutter="30">
        <el-col :sm="24" :md="16" style="transition:all .5s ease-out;margin-bottom:30px;">
          <sg-articlelist></sg-articlelist>
        </el-col>
        <el-col :sm="24" :md="8">
          <sg-rightlist></sg-rightlist>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import header from '../components/header.vue'
import articlelist from '../components/articlelist.vue'
import rightlist from '../components/rightlist.vue'

export default {
  name: 'Home',



  data() { //选项 / 数据
    return {
      state:true,
    }
  },
  methods: { //事件处理器

  },
  beforeRouteLeave (to, from, next) {
    if(to.fullPath.indexOf('=')!=-1){
      this.state=false
    }
    console.log(to.fullPath)
    next()
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  },
  components: { //定义组件
    'sg-navbar': header,
    'sg-articlelist': articlelist,
    'sg-rightlist': rightlist,
  },
  created() { //生命周期函数

  },
  mounted() {


  }
}
</script>

<style>
::-webkit-scrollbar-track {
  background: rgba(0, 0, 0, 0.1);
  border-radius: 0;
}

::-webkit-scrollbar {
  -webkit-appearance: none;
  width: 6px;
  height: 4px;
}

::-webkit-scrollbar-thumb {
  cursor: pointer;
  border-radius: 5px;
  background: #81c995;
  transition: color 0.2s ease;
}

</style>
