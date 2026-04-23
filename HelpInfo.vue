<template>
  <div style="width: 100%;height: 100%;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:-1;" src="../assets/img/twbg.jpg">
    <headInfo></headInfo>
    <!--  这是内容界面  -->
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
                <div class="oneMulu" v-if="page != item.name" @click="goInfo(item.info)">
                  <div style="width: 80%;text-align: center;">{{ item.name }}</div>
                  <img src="../assets/img/jiantou.png"
                    style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 11%;">
                </div>
                <div class="oneMuluXuan" v-else>
                  <img src="../assets/img/twCircle.png"
                    style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 7%;">
                  <div style="width: 55%;text-align: center;">
                    {{ item.name }}
                  </div>
                  <img src="../assets/img/jiantouchoose.png"
                    style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 7%;margin-left: 0.5vw;">
                  <img src="../assets/img/muluchoose.png"
                    style="width: 19vw;height: 6vw;position: absolute;bottom: -3vw;left: -3.5vw;z-index: -1;" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="rightContent">

        <!--     这里是标头   -->
        <div
          style="width: 77vw;height: 2.5vw;display: flex;position: absolute;top: 3vw;left: 3vw;justify-content: space-between;">
          <div style="display: flex;width: 15vw;">
            <div style="height: 2.5vw;;width: 2vw;margin-right: 0.8vw;">
              <img src="../assets/img/jsjt.png" style="height: 100%;object-fit: contain;width: 100%;">
            </div>
            <div
              style="height: 2.5vw;;width: 10vw;line-height: 2.5vw;;letter-spacing: 3px;font-size: 1.2vw;font-weight: bold;color: #ffffff;">
              帮助文档
            </div>
          </div>
          <div style="margin-right: 1vw;">
            <el-button
              style="height: 100%;width: 5vw;text-align: center;display:flex;justify-content: center;align-items: center;"
              type="primary" @click="openFileUpload">新增文档</el-button>
          </div>




        </div>




        <div class="rightList">

          <div class="rightListContent" v-if="this.userType == 0">
            <el-dialog :modal="false" title="上传文档" :visible.sync="showUpload" width="50%">
              <el-input class="input" v-model="textName" placeholder="请输入文档名称" style="margin-bottom: 2vh;"></el-input>
              <div style="display: flex; cursor: pointer;margin-bottom: 2vh;" @click="openFileInput">
                <el-button type="primary">选择文件</el-button>
              </div>
              <input ref="fileInput" type="file" accept=".doc, .docx" style="display: none;" @change="handleFileChange">
              <el-button @click="submit()" type="primary">确定</el-button>
            </el-dialog>
            <div class="oneRight" v-for="item in contentList" :key="item">
              <div style="width: 30%;display: flex;justify-content: start;">
                <img style="height: 0.5vw;object-fit: contain;margin-right: 1.5vw;margin-top: 2.2vw;"
                  src="../assets/img/littleBox.png">
                <div>{{ item.name }}</div>
              </div>

              <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;height: 4.6vw;margin-left: 50%;"
                @click="goXq(item.id)">
                <img src="../assets/img/jsbutton.png" style="width: 5vw;height: 1.5vw;margin-top: 1.5vw;">
                <div style="position: absolute;height: 4.6vw;line-height: 4.5vw;top: 0;left: 2vw;">查看详情</div>
              </div>
            </div>
          </div>
          <div class="rightListContent" v-if="this.userType == 1">
            <el-dialog :modal="false" title="上传文档" :visible.sync="showUpload" width="50%">
              <el-input class="input" v-model="textName" placeholder="请输入文档名称" style="margin-bottom: 2vh;"></el-input>
              <div style="display: flex; cursor: pointer;margin-bottom: 2vh;" @click="openFileInput">
                <el-button type="primary">选择文件</el-button>
              </div>
              <input ref="fileInput" type="file" accept=".doc, .docx" style="display: none;" @change="handleFileChange">
              <el-button @click="submit()" type="primary">确定</el-button>
            </el-dialog>
            <div class="oneRight" v-for="item in contentList" :key="item">

              <div style="width: 30%;display: flex;justify-content: start;">
                <img style="height: 0.5vw;object-fit: contain;margin-right: 1.5vw;margin-top: 2.2vw;"
                  src="../assets/img/littleBox.png">
                <div>{{ item.helpName }}</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;height: 4.6vw;margin-left: 40%;"
                @click="goXq(item.id)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;margin-top: 1.5vw;">
                <div style="position: absolute;height: 4.6vw;line-height: 4.5vw;top: 0vw;left: 1.7vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;margin-top: 1.5vw;">
                <div style="position: absolute;height: 4.6vw;line-height: 4.5vw;top: 0;left: 2.8vw;"
                  @click="editJs(item.id)">修改</div>
              </div>
            </div>
          </div>
          <div class="pageList">
            <page-info style="margin-left: 1vw;" v-show="total > 0" :total="total" :page.sync="pageNum"
              :limit.sync="pageSize" @pagination="getContentList()" />
          </div>
        </div>
      </div>
    </div>


    <div style="width: 100%;height: 3%;position: fixed;bottom: 0px;">
      <foot></foot>
    </div>



  </div>
</template>
<script>
import headInfo from '@/components/Head.vue';
import Foot from "@/components/Foot.vue";
import axios from "axios";
import { getToken } from "@/utils/auth";
import { getHelpList } from "@/api/kcInfo";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'HelpInfo',
  components: {
    Foot, headInfo
  },
  data() {
    return {
      userName: "",
      userType: 0,
      mulu: [
        { id: 0, name: "知识图谱", info: "Graph" },
        { id: 1, name: "辅助决策", info: "BaoGao" },
        { id: 2, name: "图文资源", info: "TwInfo" },
        { id: 3, name: "视频资源", info: "SpInfo" },
        { id: 4, name: "动画显示", info: "DhInfo" },
        { id: 5, name: "数值计算", info: "JsInfo" },
        { id: 6, name: "帮助文档", info: "HelpInfo" }
      ],
      page: "帮助文档",
      typeList: ["全部", "起降", "飞行", "通信载荷使用", "探测载荷使用", "攻击载荷使用"],
      contentList: [],
      selectName: "",
      jsType: "",
      jsType1: "",
      showUpload: false,
      pageSize: 6,
      pageNum: 1,
      total: 0,
      totalPage: 0,
      pagesList: [],
      onePagesList: [],
      openInfo: false,
      selectedFile: null,
      form: {
        name: "",
        jsType: "",
        jsInfo: "",
      },
      TxtValue: "",
      id: 0,
      textName: "",
      fileList: [], // 已上传文件列表
      isUpload: 0,
      typePic1: 0,
      //下拉框
      showOptions1: false,
      selectedOption1: null,
      options1: ["全部", "起降", "飞行", "通信载荷使用", "探测载荷使用", "攻击载荷使用"],
    }

  },
  methods: {
    openFileUpload() {
      this.showUpload = true;
    },
    goInfo(info) {
      console.log(info)
      this.$router.push('/' + info)
    },
    openFileInput() {
      this.$refs.fileInput.click();
    },
    handleFileChange(event) {
      const files = event.target.files;
      if (files && files.length > 0) {
        this.selectedFile = files[0];
      }
    },
    async submit() {
      if (!this.selectedFile) {
        alert("请选择一个文件！");
        return;
      }
      // var data = {
      //   "file": this.selectedFile,
      //   "name": this.textName
      // }
      const formData = new FormData();
      formData.append("file", this.selectedFile);
      formData.append("name", this.textName);
      console.log(getToken())
      try {
        await axios.post(
          'http://localhost:10035/kcDoc/saveHelpInfo',
          formData,
          {
            headers: {
              'Authorization': 'Bearer ' + getToken(),
              'Content-Type': 'multipart/form-data'  // 必须设置这个请求头
            },
          }
        );
        this.$message.success("上传成功");
      } catch (error) {
        console.error("上传失败", error);
        this.$message.error("上传失败");
      } finally {
        this.showUpload = false;
        this.getContentList();
      }
    },
    getContentList() {

      getHelpList().then((res) => {
        if (res.code != 500) {
          if (res.data.list != undefined) {
            this.contentList = res.data.list;
          }
        } else {
          if (res.msg == "token无效")
            localStorage.clear();
          this.$router.push('/')
        }

      })
    },
    goXq(id) {
      this.$router.push({ path: '/HelpInfoXq', query: { id: id } })
    },




  },
  mounted() {
    this.userType = localStorage.getItem("type");
    this.userName = localStorage.getItem("name");
    this.getContentList();
  }
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

.rigthHeadInfo {
  width: 100%;
}

.rightList {
  width: 92%;
  height: 78%;
  position: absolute;
  z-index: 2;
  margin-top: 9%;
  margin-left: 4.3%;
  margin-bottom: 5%;
}

.rightListContent {
  width: 100%;
  height: 92%;
  position: absolute;
  z-index: 2;
  top: 1%;

}

.oneRight {
  width: 98%;
  height: 4.6vw;
  line-height: 5vw;
  margin: 0 1%;
  display: flex;
  flex-direction: row;
  text-align: center;
  color: #ffffff;
  font-size: 1vw;
  margin-left: 7%;
}

.pageList {
  height: 2vw;
  width: 100%;
  position: absolute;
  z-index: 2;
  bottom: 0.2vw;
  display: flex;
  flex-direction: row;
  justify-content: center;


}

/* .password-input-container {
  width: 70%;
  height: 80%;
  position: absolute;
  top: 8%;
  left: 10%;
} */

/* input {
  width: 90%;
  height: 100%;
  border: none;
  outline: none;
  color: white;
  background-color: transparent;
  padding-left: 3%;
  position: absolute;
  z-index: 2000;

} */

/* input::placeholder {
  color: white;
  opacity: 1;

} */

/* .custom-select {
  position: relative;
  width: 13.5vw;
  cursor: pointer;
  height: 70%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
} */

/* .selected-option {
  text-align: center;
  line-height: 1.8vw;
  width: 8vw;
  color: #FFFFFF;
} */


/* .options {
  background-image: url("../assets/img/optionBg.png");
  background-size: 100% 100%;
  position: absolute;
  top: 110%;
  left: 0;
  right: 0;
  list-style-type: none;
  padding: 0;
  margin: 0;
  background-color: transparent;
  max-height: 150px;
  overflow-y: auto;
  z-index: 3000;
} */

/* .option {
  margin: 0.5vw;
  padding-left: 0.3vw;
  font-size: 0.7vw;
  color: #FFFFFF;

} */

/* .option:hover {
  background-image: url("../assets/img/optionSelect.png");
  background-size: 100% 100%;
  color: #000000;

} */

/*滚动条高宽度*/
/* .options::-webkit-scrollbar {
  width: 6px;
  height: 2px;
} */

/*滚动条滑块*/
/* .options::-webkit-scrollbar-thumb {
  border-radius: 3px;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  background: #76ceff;
} */

/*滚动条里面轨道*/
/* .options ::-webkit-scrollbar-track {
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.2) inset;

} */

/*滚动条的小边角*/
/* .options::-webkit-scrollbar-corner {
  background: transparent;
} */

/* .option {
  margin: 0.5vw;
  padding-left: 0.3vw;
  font-size: 0.7vw;

} */

/* .graphcontains2 {

  height: 2.5vw;
  position: relative;
  display: flex;
  flex-direction: row;
  margin-top: 0.5vw;



} */
</style>
