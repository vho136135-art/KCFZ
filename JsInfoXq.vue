<template>
  <div style="width: 100%;height: 100%;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:-1;" src="../assets/img/twbg.png">
    <headInfo :dataFinal1="this.dataFinal1"></headInfo>

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
                <div class="oneMuluXuan" v-if="item.name === '数值计算'">
                  <img src="../assets/img/twCircle.png"
                       style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 7%;">
                  <div style="width: 55%;text-align: center;">
                    {{ item.name }}
                  </div>
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
      <div class="rightContent" style="position: relative;">

        <!-- <img src="../assets/img/qjfxbg.png" style="width: 98%;height: 97.5%;position: absolute;z-index: -1;margin-left: 1%;margin-top: 0.9%;"> -->

        <DQJS v-if="currentDialog === 'DQJS'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/> 
        <SNJS v-if="currentDialog === 'SNJS'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/>
        <QJFXT v-if="currentDialog === 'QJFXT'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/>
        <!-- <JSGL v-if="currentDialog === 'JSGL'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/> -->
        <DBDLC v-if="currentDialog === 'DBDLC'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/>
        <SN1 v-if="currentDialog === 'SN1'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/>
        <LDWLT v-if="currentDialog === 'LDWLT'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/>
        <YLDQGJ v-if="currentDialog === 'YLDQGJ'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/>
        <DDZZSYFZJC v-if="currentDialog === 'DDZZSYFZJC'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/>
        <CDBTX v-if="currentDialog === 'CDBTX'" @confirm="handleDialogConfirm" @dataFinal1="handleDataFinal1"/>
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
import DQJS from "@/view/jsXqs/DQJS.vue";
import SNJS from '@/view/jsXqs/SNJS.vue';
import QJFXT from '@/view/jsXqs/QJFXT.vue';
// import JSGL from '@/view/jsXqs/JSGL.vue';
import DBDLC from '@/view/jsXqs/DBDLC.vue';
import SN1 from '@/view/jsXqs/SN1.vue';
import LDWLT from '@/view/jsXqs/LDWLT.vue';
import YLDQGJ from '@/view/jsXqs/YLDQGJ.vue';
import DDZZSYFZJC from '@/view/jsXqs/DDZZSYFZJC.vue';
import CDBTX from "@/view/jsXqs/CDBTX.vue";
// import {fileUpdate} from "@/api/file";
// import {fileUpdate} from "@/api/file";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'JsInfoXq',
  components: {Foot, headInfo, DQJS, SNJS, QJFXT, DBDLC,SN1,LDWLT,YLDQGJ,DDZZSYFZJC,CDBTX},
  data() {
    return {
      docId: undefined,
      level: 0,
      url: "",
      userName: "",
      dataFinal1: {},
      currentDialog: '',
      mulu: [
        { id: 0, name: "知识图谱", info: "Graph" },
        { id: 1, name: "辅助决策", info: "BaoGao" },
        { id: 2, name: "图文资源", info: "TwInfo" },
        { id: 3, name: "视频资源", info: "SpInfo" },
        { id: 4, name: "动画显示", info: "DhInfo" },
        { id: 5, name: "数值计算", info: "JsInfo" },
        { id: 6, name: "帮助文档", info: "HelpInfo" }
      ],
      contentInfo: {
        title: "",
        content: ""
      },
    }
  },
  methods: {
    //   dataURLtoBlob(dataURL) {
    //     const arr = dataURL.split(',');
    //     const mime = arr[0].match(/:(.*?);/)[1];
    //     const bstr = atob(arr[1]);
    //     let n = bstr.length;
    //     const u8arr = new Uint8Array(n);
    //
    //     while (n--) {
    //       u8arr[n] = bstr.charCodeAt(n);
    //     }
    //
    //     return new Blob([u8arr], {type: mime});
    //   },
    //   handleCapture(dataURL) {
    //
    //     const blob = this.dataURLtoBlob(dataURL);
    //     // 3. 创建FormData并添加文件
    //     const formData = new FormData();
    //     formData.append('file', blob, 'screenshot.png');
    //     formData.append('additionalData', '任何其他表单数据');
    //
    //     // 4. 上传到服务器
    //     fileUpdate(blob).then((res)=>{
    //       console.log(res.data.url);
    //       this.dataFinal1.allImg = res.data.url
    //     })
    //
    //
    //
    // },

    goInfo(info) {
      console.log(info)
      this.$router.push('/' + info)
    },
    getInfo() {
      var data = {
        id: this.docId
      }
      getInfo(data).then((res) => {
        console.log(res)
        if (res.data && res.data.data && res.data.data.jsInfo) {
          this.currentDialog = res.data.data.jsInfo.toUpperCase();
        }
      })
    },
    // handleDataFinal1(data) {
    //   this.dataFinal1 = data;
    //   console.log(this.dataFinal1)
    //   this.dataFinal1.jsId = this.$route.query.id;
    //   console.log(this.dataFinal1)
    // },
    handleDialogConfirm() {
      this.currentDialog = '';
    },
  }
  ,
  mounted() {
    this.docId = this.$route.query.id;
    this.userType = localStorage.getItem("type");
    this.userName = localStorage.getItem("name");
    if (this.docId) {
      this.getInfo();
    }
  }
  ,
}
</script>
<style scoped>
.content {
  width: 100%;
  height: 86%;
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
  /* background-color: #7cdeff; */
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
  font-size: 1vw;
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
  font-size: 1vw;
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
</style>
