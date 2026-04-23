<template>
  <div style="width: 100%;height: 100%;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:-1;" src="../assets/img/spbg.jpg">
    <headInfo style="position: absolute;z-index: 100"></headInfo>
    <div class="content">
      <div class="leftContent">
        <div class="leftBox1">
          <div style="width: 50%;margin: 0 auto;">
            <p style="font-size: 1vw;">Hi,{{ userName }}~</p>
            <p style="font-size: 0.7vw;">欢迎使用XXXX辅助决策</p>
          </div>
        </div>
        <div class="leftBox2">
          <div class="muluBox">
            <div class="muluList">
              <div v-for="item in mulu" :key="item">
                <div class="oneMuluXuan" v-if="item.name === '动画显示'">
                  <img src="../assets/img/twCircle.png"
                       style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 7%;">
                  <div style="width: 55%;text-align: center;">
                    {{ item.name }}</div>
                  <img src="../assets/img/jiantouchoose.png"
                       style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 7%;">
                  <img src="../assets/img/muluchoose.png"
                       style="width: 19vw;height: 6vw;position: absolute;bottom: -3vw;left: -3.5vw;z-index: -1;"/>
                </div>
                <div class="oneMulu" v-else @click="goInfo(item.info)">
                  <div style="width: 80%;text-align: center;">{{ item.name }}</div>
                  <img src="../assets/img/jiantou.png"
                       style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 13%;">
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="rightContent">
        <div class="contentTitle" style="white-space: nowrap;">{{contentInfo.title}}</div>
        <div class="contentInfo">

          <div class="contentText">
            <Video1 style="height: 90%; object-fit:contain" :src="contentInfo.url"
                    :second="3"/>
          </div>
        </div>
      </div>
    </div>
    <div style="width: 100%;height: 3%;position: fixed;bottom: 0px;z-index: 100">
      <foot></foot>
    </div>
  </div>

</template>
<script>

import headInfo from "@/components/Head.vue";
import Foot from "@/components/Foot.vue";
import {getInfo} from "@/api/kcInfo";
import Video1 from "@/components/Video1.vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'DhInfoXq',
  components: {Video1, Foot, headInfo},
  data() {
    return{
      docId:undefined,
      level:0,
      url:"",
      userName:"",
      mulu: [
        { id: 0, name: "知识图谱", info: "Graph" },
        { id: 1, name: "辅助决策", info: "BaoGao" },
        { id: 2, name: "图文资源", info: "TwInfo" },
        { id: 3, name: "视频资源", info: "SpInfo" },
        { id: 4, name: "动画显示", info: "DhInfo" },
        { id: 5, name: "数值计算", info: "JsInfo" },
        { id: 6, name: "帮助文档", info: "HelpInfo" }
      ],
      contentInfo:{
        title:"",
        url:""
      },

    }
  },
  methods:{
    goInfo(info) {

      this.$router.push('/' + info)
    },
    getXqInfo(){
      var data = {
        id:this.docId
      }
      getInfo(data).then((res)=>{
         console.log(res);
         this.contentInfo.url = res.data.data.dwUrl;
         this.contentInfo.title = res.data.data.name

      })
    }
  },
  mounted() {
    this.docId = this.$route.query.id;
    this.userType = localStorage.getItem("type");
    this.userName = localStorage.getItem("name");
    this.getXqInfo();
  }
}
</script>
<style scoped>
.content {
  width: 100%;
  height: 86%;
  padding-top: 5%;
}

.leftContent {
  width: 14%;
  height: 100%;
  float: left;
}

.leftBox1 {
  width: 100%;
  height: 10%;
  margin-top: -5%;
  color: #7cdeff;
}

.leftBox2 {
  width: 100%;
  height: 90%;
}

.muluBox {
  margin: 0 14%;
  height: 92%;
  width: 72%;
  position: relative;
  margin-top: 5%;
}

.muluList {
  width: 100%;
  height: 90%;
  //background-color: #7cdeff;
  display: flex;
  flex-direction: column;
  position: absolute;
  z-index: 2;
  margin-top: 20%;

}

.oneMulu {
  width: 80%;
  height: 2.5vw;
  line-height: 2.5vw;
  font-size: 0.9vw;
  border-bottom: 1px solid rgba(112, 192, 227, 0.47);
  margin-left: 10%;
  color: #d1d3d7;
  display: flex;
  flex-direction: row;

}

.oneMuluXuan {

  width: 90%;
  height: 2.5vw;
  line-height: 2.1vw;
  font-size: 0.9vw;
  color: #13ffff;
  display: flex;
  flex-direction: row;
  padding-left: 10%;
  position: relative;

}


.rightContent {
  width: 84%;
  height: 100%;
  float: left;
  position: relative;
}

.contentInfo{
  width: 90%;
  height: 82.5%;
  margin-left: 5.7%;
  position: absolute;
  z-index: 101;
  margin-top: 5.2%;
  border-radius: 1vw;
  //background-color: #FFFFFF;
}

.contentTitle{
  width: 20vw;
  height: 3vw;
  margin-top: 0.5%;
  font-size: 1.5vw;
  color: #ffffff;

  text-align: center;
  letter-spacing: 5px;
  position: absolute;
  top: 0.5vw;
  margin-left: 36%;
  line-height:3vw;
  font-family: 'Helvetica Neue', 'Helvetica', 'Arial', sans-serif;


}
.contentText{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  margin-top: 4%;

}
.m-video{

  background: none !important;
}
</style>
