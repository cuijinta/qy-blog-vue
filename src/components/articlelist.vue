<!-- 文章列表 -->
<template>
  <el-row class="sharelistBox" >

    <el-col :span="24" class="s-item tcommonBox11" type="flex"  v-for="(item,index) in articleList" :key="'article'+index">
            <span class="s-round-date">
        <span
          class="month"
          v-html="showInitDate(item.createTime, 'month') + '月'"
        ></span>
        <span class="day" v-html="showInitDate(item.createTime, 'date')"></span>
      </span>
      <header>
        <div class="ui2 label2">
          <a :href="'#/Share?classId='+item.categoryId">{{item.categoryName}}</a>
        </div>
      </header>
      <h2 class="ddy">
        <i class="fa fa-fw fa-user"></i>发表于
        <i class="fa fa-fw fa-clock-o"></i><span v-html="showInitDate(item.createTime,'all')">{{showInitDate(item.createTime,'all')}}</span> •
        <i class="fa fa-fw fa-eye"></i>{{item.viewCount}} 次围观 •
      </h2>
      <div class="article-content1">
     <a  class='imgs' :href="'#/DetailArticle?aid='+item.id" >
       <p  style="overflow:hidden;text-align:center;" class="img" >
<!--          <img :src="item.thumbnail" alt="" class="maxW">-->
          <img :src="require('@/assets/logo.png')"  alt=""/>

        </p>
     </a>
        <div  class='text' style="text-indent:2em;">
          <h3>
            <a :href="'#/DetailArticle?aid='+item.id">
              {{item.title}}
            </a>
          </h3>
          {{item.summary}}ewwwwwddddddddddddddddddddddeewwwwwdddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddewwwwwdddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddwwwwwdddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddd
        </div>
      </div>

<!--      <div class="viewdetail">-->
<!--        <a class="tcolors-bg" :href="'#/DetailArticle?aid='+item.id" target="_blank">-->
<!--          阅读全文>>-->
<!--        </a>-->
<!--      </div>-->

    </el-col>
    <el-col class="viewmore">
      <a v-show="hasMore" class="tcolors-bg" href="javascript:void(0);" @click="addMoreFun">点击加载更多</a>
      <a v-show="!hasMore" class="tcolors-bg" href="javascript:void(0);">暂无更多数据</a>
    </el-col>
  </el-row>
</template>

<script>
import {initDate} from '../utils/server.js'
import {articleList} from '../api/article'
import router from "../router";
export default {
  name:'Share',
  data() { //选项 / 数据
    return {
      // 查询参数
      queryParams: {
        pageNum: 1,
        pageSize: 10,
        categoryId: null
      },
      articleList:[],
      hasMore:true
    }
  },

  methods: {
    // gogogo(id){
    //   router.push({
    //     path:'/DetailArticle',
    //     query:{'aid':id}
    //   })
    // },
    //事件处理器
    showInitDate: function(oldDate,full){
      return initDate(oldDate,full)
    },
    getList(){
      articleList(this.queryParams).then((response)=>{
        this.articleList = this.articleList.concat(response.rows)
        if(response.total<=this.articleList.length){
          this.hasMore=false
        }else{
          this.hasMore=true
          this.queryParams.pageNum++
        }
      })
    },
    showSearchShowList:function(initData){//展示数据
      if(initData){
        this.articleList = []

      }
      this.getList()
    },
    addMoreFun:function(){//查看更多
      this.showSearchShowList(false);
    },
    routeChange:function(){
      var that = this;
      this.queryParams.categoryId = (that.$route.query.classId==undefined?null:parseInt(that.$route.query.classId));//获取传参的classId
      this.showSearchShowList(true);
    }
  },
  components: { //定义组件

  },
  watch: {
    // 如果路由有变化，会再次执行该方法
    '$route':'routeChange',
    '$store.state.keywords':'routeChange'
  },
  created() { //生命周期函数
    // console.log(this.$route);
    var that = this;
    that.routeChange();
  }
}
</script>

<style >
.ui2.label2 {
  position: absolute !important;
  right: -20px !important;
  transform: translate(0,-30%);
  padding-right: 18px!important;
}
.ui2.label2::after {
  border: none!important;
}
.ui2.label2 {
  border-color: #81c995;
  -webkit-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.2), 0 1px 5px 0 rgba(0, 0, 0, 0.12);
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.2), 0 1px 5px 0 rgba(0, 0, 0, 0.12);
  background-color: #ee675c;
  margin: 5px 0 15px 2px;
  font-size: 14px;

  border-radius: 0 4px 4px 0;
  padding: 7px 11.2px 7px 32px;
  display: inline-block;
  color: #fff;
}
.ui2.label2::after {
  position: absolute;
  content: '';
  top: 100%;
  left: 0;
  border-top: 0 solid transparent;
  border-right-width: 1em;
  border-right-color: #48456D;
  border-right-style: solid;
  border-bottom: 1em solid transparent;
  border-left: 0 solid transparent;
  width: 0;
  height: 0;
}
.ui2.label2 a {
  color: #fff;
  line-height: 100%;
}
.tcommonBox11{

  white-space: normal;
  word-wrap: break-word;
  word-break: break-all;
  position: relative;
  background: #ffffff;
  padding:15px;
  border-radius: 5px;
  margin-bottom: 40px;
  font-size: 15px;
}
.tcommonBox11 header{
  position: relative;
  white-space: normal;
  word-wrap: break-word;
  word-break: break-all;
}

.tcommonBox11 header h2{
  margin:10px 0;
  line-height: 24px;
  text-align: center;
  color:#555;
  font-size: 14px;
}
.tcommonBox11 section p{
  line-height: 24px;
  margin:10px 0;
}
.tcommonBox11  header h2 .el-rate,.rateBox{
  display:inline-block;
}
.tcommonBox11  header h2 .el-rate i{
  font-size: 16px;
}
/*分享标题*/
.shareTitle{
  margin-bottom: 40px;
  position: relative;
  border-radius: 5px;
  background: #fff;
  padding:15px;
}
.shareclassTwo{
  width:100%;
}
.shareclassTwo li{
  display: inline-block;
}
.shareclassTwo li a{
  display: inline-block;
  padding:3px 7px;
  margin:5px 10px;
  color:#fff;
  border-radius: 4px;
  background: #64609E;
  border: 1px solid #64609E;
  transition: transform 0.2s linear;
  -webkit-transition: transform 0.2s linear;
}
.shareclassTwo li a:hover{
  transform: translate(0,-3px);
  -webkit-transform: translate(0,-3px);
}
.shareclassTwo li a.active{
  background: #fff;
  color:#64609E;

}
.article-content1{
  margin-top: 24px;
  display: flex;
  flex-direction: row;
  gap:0 20px;
}
.article-content1 .imgs  {
  position: relative;
  height: 100px;
  flex: 1;
 border: #8c939d 1px solid;
  border-radius:20px ;
}
.article-content1 .imgs .img{
  margin-top: 0;
  position: relative;
  width: 100%;
  height: 100px;

}
.article-content1 .imgs .img img{
  object-fit:contain;
  width: 100%;
  height: 100%;

}
.article-content1 .text{
  flex: 3;
  word-wrap: break-word;
  word-break: normal;
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  text-overflow: ellipsis;
  max-height: 66px;
}
.article-content1 .text h3{
  margin: 10px 0 8px 0;
  font-size: 20px;
  font-weight: 700;
  text-align: center;
  line-height: 14px;
}
/*文章列表*/
.sharelistBox{
  transition: all 0.5s ease-out;
  font-size: 15px;
}
.ddy{
  overflow: hidden;
  width: 75%;
  text-align: center;
  position: absolute;
  left:25%;
  top:74%;

}
/*.sharelistBox .viewmore a:hover,.s-item .viewdetail a:hover{
    background: #48456C;
}*/
</style>
