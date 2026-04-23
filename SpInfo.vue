<template>
  <div style="width: 100%;height: 100%;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:-1;" src="../assets/img/twbg.png">
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
        <div class="rigthHeadInfo" style="position: relative;">
          <div style="width: 30%;height: 2.2vw;position: absolute;top: 2.2vw;right: 1vw;">
            <div class="password-input-container">
              <img src="../assets/img/search.png" style="position: absolute;z-index: -1;width: 100%;height: 100%;">

              <input type="text" placeholder="请输入" v-model="selectName" @keyup.enter="getContentList()" style="width: 86%;" />
            </div>
            <div style="width: 6%;height: 70%;float: right;margin-right: 18%;margin-top: 1%;cursor:pointer" @click="getContentList()">
              <img src="../assets/img/look.png" style="width: 100%;height: 100%;">
            </div>

          </div>
          <div
            style="display: flex;flex-direction: row;position: absolute;z-index: 1;margin-top: 3.2vw;margin-left: 3.6%;cursor: pointer;">
            <div v-for="item in typeList" :key="item" style="position: relative;margin-right: 1vw;"
              @click="changeType(item)">

              <img v-if="spType1 == item" src="../assets/img/typePicTestChoose.png"
                style="width: 8.5vw;object-fit: contain;">
              <img v-else src="../assets/img/typePicTest.png" style="width: 8.5vw;object-fit: contain;">

              <div
                style="position: absolute;z-index: 12121;width: 100%;text-align: center;color: white;top: 15%;font-size: 1vw;">
                {{ item }}
              </div>
            </div>
          </div>
          <div
            style="width: 94.7%;height:3vw;position: absolute;z-index: 1;top: 4.9vw;left: 2.5%;background-color: rgba(85,174,248,0.22);border-radius: 1vw 1vw 0 0">
          </div>
          <div
            style="width: 94.4%;height: 2.9vw;position: absolute;z-index: 2;margin-left: 2.6%;top: 5vw;font-size: 1vw;"
            v-if="this.userType == 1">
            <div
              style="width: 100%;height: 100%;display: flex;flex-direction: row;line-height: 2.9vw;text-align: center;color: #ffffff;">
              <div style="width: 10%;">序号</div>
              <div style="width: 20%;">标题</div>
              <div style="width: 60%;">视频</div>
              <div style="width: 10%;">详情</div>
              <div style="width: 10%;">操作</div>
            </div>
          </div>
          <div
            style="width: 94.4%;height: 2.9vw;position: absolute;z-index: 2;margin-left: 2.6%;top: 5vw;font-size: 1vw;"
            v-if="this.userType == 0">
            <div
              style="width: 100%;height: 100%;display: flex;flex-direction: row;line-height: 2.9vw;text-align: center;color: #ffffff;">
              <div style="width: 10%;">序号</div>
              <div style="width: 20%;">标题</div>
              <div style="width: 60%;">视频</div>
              <div style="width: 10%;">详情</div>
            </div>
          </div>
        </div>
        <div class="rightList">

          <div class="rightListContent" v-if="this.userType == 0">
            <div class="oneRight" v-for="item in contentList" :key="item">
              <div style="width: 8%;">{{ item.index }}</div>
              <div style="width: 22%;white-space: nowrap;">{{ item.name }}</div>
              <div
                style="width: 60%;display: flex;flex-direction: row;justify-content: space-around;position: relative;">
                <Video1
                  style="height: 100%; object-fit:contain;display: flex;justify-content: center;width: 8vw;background: none !important;"
                  :src="item.spUrl" :second="3" :controls="false" disablePictureInPicture class="video" />
                <div
                  style="position: absolute;top: 0;left: 0;width: 100%;height: 100%;background: transparent;cursor: pointer;z-index: 10;"
                  @click="goXq(item.id)"></div>
              </div>
              <div style="width: 10%;text-decoration: underline;font-style: italic;cursor: pointer;" @click="goXq(item.id)">
                点击查看详情
              </div>
            </div>
          </div>
          <div class="rightListContent" v-if="this.userType == 1">
            <div class="oneRight" v-for="item in contentList" :key="item">
              <div style="width: 8%;">{{ item.index }}</div>
              <div style="width: 22%;white-space: nowrap;">{{ item.name }}</div>
              <div
                style="width: 60%;display: flex;flex-direction: row;justify-content: space-around;position: relative;">
                <!-- <div style="position: relative; width: 100%; height: 100%;"> -->
                <Video1
                  style="height: 90%; object-fit:contain;display: flex;justify-content: center;width: 8vw;background: none !important;"
                  :src="item.spUrl" :second="3" :controls="false" disablePictureInPicture class="video" />
                <div
                  style="position: absolute;top: 0;left: 0;width: 100%;height: 100%;background: transparent;cursor: pointer;z-index: 10;"
                  @click="goXq(item.id)"></div>
                <!-- </div> -->

              </div>
              <div style="width: 10%;text-decoration: underline;font-style: italic;cursor: pointer;" @click="goXq(item.id)">
                点击查看详情
              </div>
              <div
                style="width: 9%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;margin-left: 1%;cursor: pointer;">
                <div @click="editTw(item.id)">修改</div>
                <!--                <div @click="deleteTw(item.id)">删除</div>-->
              </div>
            </div>
          </div>
          <div class="pageList">
            <page-info v-if="showPage" style="margin-left: 1vw;" :total="total" :page.sync="pageNum"
              :limit.sync="pageSize" @pagination="handlePagination()" />
          </div>
        </div>
      </div>
    </div>


    <div style="width: 100%;height: 3%;position: fixed;bottom: 0px;">
      <foot></foot>
    </div>

    <el-dialog :visible.sync="openInfo" title="视频" top="3vw">
      <el-form :model="form" label-width="80px">
        <el-form-item label="视频名称">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item style="position: relative ;" label="选择类别">
          <el-select v-model="form.spType" placeholder="请选择类别">
            <el-option v-for="item in typeList" :key="item" :label="item" :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="上传视频" prop="courseUrl">
          <el-upload class="avatar-uploader el-upload--text" multiple :headers="videoUpload.headers"
            :action="videoUpload.url" :file-list="videoFileList" :show-file-list="false" accept=".mp4"
            :on-success="handleVideoSuccess" :before-upload="beforeUploadVideo" :on-progress="uploadVideoProcess"
            :on-remove="handleVideoRemove">
            <div v-if="!videoFlag && showVideoPath" style="display: flex; flex-wrap: wrap; gap: 10px;">
              <div style="position: relative; flex: 1 1 calc(33.333% - 20px); min-width: 200px; margin-bottom: 10px;">
                <video :src="showVideoPath" style="width:90%; height: auto;border-radius: 0.5vw;"
                  class="avatar video-avatar" controls>
                  您的浏览器不支持视频播放
                </video>
                <img src="../assets/img/delete.png" @click.stop="handleVideoRemove(videoFileList[0])"
                  style="width: 35px; height: 35px;position: absolute; top: 5px; left: 5px; cursor: pointer; z-index: 999;"
                  alt="删除" />
              </div>
            </div>
            <el-progress :stroke-width="10" class="progressType" v-if="videoFlag" type="circle"
              :percentage="videoUploadPercent" style="margin-top:30px;"></el-progress>
            <el-button style="z-index: 999;" class="video-btn" slot="trigger" size="small" type="primary">点击上传视频
            </el-button>
          </el-upload>

        </el-form-item>
      </el-form>


      <div slot="footer" class="dialog-footer" style="margin-top: 2vw;">
        <el-button @click="openInfo = false">取 消</el-button>
        <el-button type="primary" @click="submitInfo">确 定</el-button>
      </div>
    </el-dialog>


  </div>

</template>
<script>
import headInfo from '@/components/Head.vue';
import Foot from "@/components/Foot.vue";
import { editInfo, getSpList, getInfo, getByParentIdAndType } from "@/api/kcInfo";
import { getToken } from "@/utils/auth";
import Video1 from "@/components/Video1.vue";
import { twdelete } from "@/api/twdelete";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'SpInfo',
  components: {
    Video1,

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
      page: "视频资源",
      typeList: ["全部", "起降", "飞行", "通信载荷使用", "探测载荷使用", "攻击载荷使用"],
      contentList: [],
      selectName: "",
      spType1: "全部",
      spType: "",
      pageSize: 5,
      pageNum: 1,
      total: 0,
      showPage: false,
      totalPage: 0,
      pagesList: [],
      onePagesList: [],
      openInfo: false,


      form: {
        name: "",
        contentInfo: "",
        spType: "",
      },
      TxtValue: "",
      id: 0,
      fileList: [], // 已上传文件列表
      isUpload: 0,
      contentListAll:[],

      //上传的视频
      videoUpload: {
        // 设置上传的请求头部
        headers: { Authorization: "Bearer " + getToken() },
        // 上传的地址
        url: "http://127.0.0.1:10035/fileUpdate/upload",
        url2: "http://127.0.0.1:10035",
      },
      videoFlag: false, //是否显示进度条
      videoUploadPercent: "", //进度条的进度，
      isShowUploadVideo: false, //显示上传按钮
      videoFileList: [],
      showVideoPath: "",
      uploadUrl: "",//你要上传视频到你后台的地址
    }

  },
  methods: {
    handlePagination() {
      if (this.$route.query.parentId != null && this.$route.query.parentId != undefined) {
        console.log("dhsajdhjsagdhjasgdjhgas")
        this.pageSize = 5;
        this.total = this.contentListAll.length;
        console.log(this.total)
        console.log(this.pageSize)
        this.totalPage = Math.ceil(this.total / this.pageSize);
        console.log(this.contentListAll)
        
        const startIndex = (this.pageNum - 1) * this.pageSize;
        const endIndex = Math.min(startIndex + this.pageSize, this.contentListAll.length);

        // 获取当前页数据
        this.contentList = this.contentListAll.slice(startIndex, endIndex);
        for(let i = 0; i < this.contentList.length;i++){
          var c = this.contentList[i];
          c.index = (this.pageNum - 1) * this.pageSize + i + 1;
        }
        console.log( this.contentList)


      } else {
        this.getContentList();
      }
    },
    goInfo(info) {
      console.log(info)
      this.$router.push('/' + info)
    },
    changeType(item) {
      this.spType1 = item;
      if (this.spType1 == "全部") {
        this.spType = "";
      } else {
        this.spType = this.spType1
      }
      this.getContentList();
    },
    choosePage(item) {
      console.log(item);
      this.pageNum = item;
      this.getContentList();
    },
    getContentList() {

      var data = {
        name: this.selectName,
        spType: this.spType,
        pageNum: this.pageNum,
        pageSize: this.pageSize
      }
      getSpList(data).then((res) => {
        if (res.code != 500) {
          if (res.data.list != undefined) {
            this.contentList = res.data.list;
            this.total = res.data.total;
            this.totalPage = res.data.totalPages;
            for(let i = 0;i < this.contentList.length;i++){
              var c1 = this.contentList[i];
              c1.index = (this.pageNum - 1) * this.pageSize + i + 1;
            }
            var aaa = 0;
            this.onePagesList = [];
            this.pagesList = [];
            if (this.totalPage > 3) {
              if (this.pageNum < this.totalPage - 3) {

                for (let i = this.pageNum; i <= this.totalPage; i++) {
                  this.pagesList.push(i);
                  this.onePagesList.push(i);
                  aaa = aaa + 1;
                  console.log(aaa);
                  if (aaa == 4) {
                    break;
                  }
                }
              }
            } else {
              for (let i = 1; i <= this.totalPage; i++) {

                this.pagesList.push(i);
                this.onePagesList.push(i);
                aaa = aaa + 1;
                console.log(aaa);
                if (aaa == 3) {
                  break;
                }
              }
            }


            console.log(this.onePagesList)
          }

        } else {
          if (res.msg == "token无效")
            localStorage.clear();
          this.$router.push('/')
        }


      })
    },
    goXq(id) {

      this.$router.push({ path: '/SpInfoXq', query: { id: id, type: "sp" } })
      localStorage.setItem("pageNum", this.pageNum)

    },


    //管理员操作
    //管理员操作
    deleteTw(id) {
      twdelete(id);
      this.getContentList();
      console.log("这是删除操作")
    },
    editTw(id) {
      //展示出一个修改的弹窗
      var data = {
        id: id
      }
      getInfo(data).then((res) => {

        this.openInfo = true;
        this.form.name = res.data.data.name;
        this.form.spType = res.data.data.spType
        this.id = id;

        this.videoFileList = [];
        this.showVideoPath = "";
        if (res.data.data.spUrl != null) {
          this.videoFileList.push({ url: res.data.data.spUrl, name: res.data.data.name });
          this.showVideoPath = res.data.data.spUrl;
        }


      })

    },


    //视频
    beforeUploadVideo(file) {
      const isLt1024M = (file.size / 1024 / 1024) < 1024;
      this.form.videoSize = file.size / 1024 / 1024;
      //判断是不是MP4格式视频
      if (['video/mp4'].indexOf(file.type) === -1) {
        this.$message.error('请上传正确的视频格式');
        return false;
      }
      //单个视频大小限制在1024M以内
      if (!isLt1024M) {
        this.$message.error('上传视频大小不能超过1024MB哦!');
        return false;
      }
      return true;
    },
    // eslint-disable-next-line no-unused-vars
    uploadVideoProcess(event, file, fileList) {
      this.videoFlag = true;
      this.videoUploadPercent = file.percentage.toFixed(0) * 1;
    },
    updateCourseUrl() {
      this.form.courseUrl = this.showVideoPath;
      console.log('Updated courseUrl:', this.form.courseUrl);
    },

    // 上传成功回调
    // eslint-disable-next-line no-unused-vars
    handleVideoSuccess(response, file, fileList) {
      console.log(response.data.url)
      try {
        // 确保res是一个非空字符串
        if (!response.data.url || typeof response.data.url !== 'string') {
          this.$message.error('视频上传失败，请检查服务器响应');
          return;
        }
        const videoUrl = response.data.url.trim();
        if (videoUrl === '') {
          this.$message.error('收到无效的视频URL，请检查服务器响应');
          return;
        }
        // 检查重复
        if (this.videoFileList.some(video => video.url === videoUrl)) {
          this.$message.warning('该视频已存在于列表中');
          return;
        }
        this.videoFileList.push({ url: videoUrl, name: file.name });
        this.showVideoPath = this.videoFileList.map(f => f.url).join(',');
        this.updateCourseUrl();
        this.$message.success('视频上传成功');
        console.log('Updated videoFileList:', this.videoFileList);
        console.log('Updated showVideoPath:', this.showVideoPath);
        this.$nextTick(() => {
          this.videoFlag = false;
        });
      } catch (error) {
        this.$message.error('处理上传响应时发生错误：' + error.message);
        console.error('Error in handleVideoSuccess:', error);
      }
    },
    handleVideoRemove(video) {
      if (!video) return;
      // 使用uid唯一标识符进行匹配
      const index = this.videoFileList.findIndex(item => item.uid === video.uid);
      if (index > -1) { // 更新UI
        this.videoFileList.splice(index, 1);
        this.showVideoPath = this.videoFileList.map(f => f.url).join(',');
        this.updateCourseUrl();
      }
    },
    // 上传失败后的回调
    // eslint-disable-next-line no-unused-vars
    handleError(err, file, fileList) {
      console.log('Upload error:', err);
      this.$message.error('上传失败，请重试！');
    },
    submitInfo() {
      console.log(this.videoFileList);
      if (this.form.spType == "全部") {
        this.form.spType = "";
      }
      var urlStr = this.videoFileList[0];
      var data = {
        name: this.form.name,
        spUrl: urlStr.url,
        type: 2,
        id: this.id,
        spType: this.form.spType
      }
      editInfo(data).then((res) => {
        console.log(res);
        this.openInfo = false;
        this.getContentList();
      })
    }
  },
  mounted() {
    this.userType = localStorage.getItem("type");
    this.userName = localStorage.getItem("name");
    const savedPageNum = localStorage.getItem("pageNum");
    this.pageNum = savedPageNum ? parseInt(savedPageNum, 10) : 1; // 转换为数字，默认值为1
    console.log("Restored pageNum:", this.pageNum);
    this.showPage = true
    this.$nextTick(() => {
      console.log("PageNum after nextTick:", this.pageNum);
      const parentId = this.$route.query.parentId;
      const type = this.$route.query.type;
      if (parentId != null && parentId != undefined) {
        var data = {
          parentId: parentId,
          type: type,
          pageNum: this.pageNum,
          pageSize: this.pageSize
        }
        getByParentIdAndType(data).then((res) => {
          console.log(res,data.list)
          this.contentList = res.data.list;
          this.total = res.data.total;
          this.totalPage = res.data.totalPages;
          this.onePagesList = [];
          this.pagesList = [];
          // this.updateOnePagesList();
          console.log(this.contentList)
          this.contentListAll = this.contentList
          this.handlePagination();
        })
      } else {
        this.getContentList();
      }
      localStorage.setItem("pageNum", 1)
    });
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
  width: 94.6%;
  height: 77%;
  position: absolute;
  z-index: 2;
  //background-color: #42b983;
  margin-top: 10%;
  margin-left: 2.6%;
  margin-bottom: 5%;
  border-radius: 0 0 1vw 1vw;
  background-color: rgba(85, 174, 248, 0.22);
}

.rightListContent {
  width: 100%;
  height: 100%;
  position: absolute;
  z-index: 2;
  top: 1%;

}

.oneRight {
  width: 98%;
  height: 5vw;
  line-height: 5vw;
  //background-color: #42b983;
  margin: 0 1%;
  display: flex;
  flex-direction: row;
  text-align: center;
  color: #ffffff;
  font-size: 1vw;
  margin-top: 1%;
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

.password-input-container {
  width: 63%;
  height: 80%;
  //background: #b94289;
  position: absolute;
  top: 8%;
  left: 10%;
}

input {
  width: 90%;
  height: 100%;
  border: none;
  outline: none;
  color: white;
  /* 文字颜色 */
  background-color: transparent;
  padding-left: 3%;
  position: absolute;
  z-index: 2000;

}

input::placeholder {
  color: white;
  opacity: 1;
  /* Firefox 默认将 placeholder 的透明度设置为 0.54 */

}

.m-video video u-video-hover {
  width: 8vw !important;
  background: none !important;
}
</style>
