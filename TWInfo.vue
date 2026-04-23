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
              <div v-for="item in mulu" :key="item.id">
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

              <input type="text" placeholder="请输入" v-model="selectName" @keyup.enter="getContentList()" />
            </div>
            <div style="width: 6%;height: 70%;float: right;margin-right: 18%;margin-top: 1%;cursor: pointer;" @click="getContentList()">
              <img src="../assets/img/look.png" style="width: 100%;height: 100%;pointer-events: none;">
            </div>

          </div>
          <div
            style="display: flex;flex-direction: row;position: absolute;z-index: 1;margin-top: 3.2vw;margin-left: 3.6%;cursor: pointer;">
            <div v-for="item in typeList" :key="item" style="position: relative;margin-right: 1vw;"
              @click="changeType(item)">

              <img v-if="twType1 == item" src="../assets/img/typePicTestChoose.png"
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
              <div style="width: 60%;">图片</div>
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
              <div style="width: 60%;">图片</div>
              <div style="width: 10%;">详情</div>
            </div>
          </div>
        </div>
        <div class="rightList">

             

          <div class="rightListContent" v-if="this.userType == 0">
            <div class="oneRight" v-for="item in contentList" :key="item.id">
              <div style="width: 8%;">{{ item.index }}</div>
              <div style="width: 22%;">{{ item.name }}</div>
              <div style="width: 60%;display: flex;flex-direction: row;justify-content: center;">
                <div v-for="item1 in item.imgss.slice(0, 4)" :key="item1">
                  <img :src="item1"
                    style="height: 4vw;object-fit: contain;justify-content: flex-start;margin-left: 1vw;border-radius: 1vw;max-width: 4vw">
                </div>
              </div>
              <div style="width: 10%;text-decoration: underline;font-style: italic;cursor: pointer;" @click="goXq(item.id)">
                点击查看详情
              </div>
            </div>
          </div>
          <div class="rightListContent" v-if="this.userType == 1">
        
            <div class="oneRight" v-for="item in contentList" :key="item.id">
              <div style="width: 8%;">{{ item.index }}</div>
              <div style="width: 22%;">{{ item.name }}</div>
              <div style="width: 60%;display: flex;flex-direction: row;justify-content: center;" v-if="item.imgss !=null && item.imgss.length>4">
                <div v-for="item1 in item.imgss.slice(0, 4)" :key="item1">
                  <img :src="item1"
                    style="height: 4vw;object-fit: contain;justify-content: flex-start;margin-left: 1vw;border-radius: 1vw;max-width: 10vw">
                </div>
              </div>
             
              <div style="width: 60%;display: flex;flex-direction: row;justify-content: center;" v-else>
                <div v-for="item1 in item.imgss" :key="item1">
                  <img :src="item1"
                    style="height: 4vw;object-fit: contain;justify-content: flex-start;margin-left: 1vw;border-radius: 1vw;max-width: 10vw">
                </div>
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
    <!--            <div style="float: left;margin-right: 0.1vw;" @click="choosePage(onePagesList[0]-1)">...</div>-->
    <!--            <div v-for="item in onePagesList" :key="item" @click="choosePage(item)" style="margin-left: 1vw;">-->
    <!--              <img src="../assets/img/pageChoose.png" style="position: absolute;z-index: -1">-->
    <!--              <div style="width: 1.2vw;height: 1.2vw;margin-top: 0.15vw;font-size: 0.5vw;-->
    <!--                   text-align: center;line-height: 1.2vw;margin-right: 1vw;">-->
    <!--                {{ item }}-->
    <!--              </div>-->
    <!--            </div>-->
    <!--            <div style="float: left;margin-left: 0.1vw;">...</div>-->

    <div style="width: 100%;height: 3%;position: fixed;bottom: 0px;">
      <foot></foot>
    </div>

    <el-dialog :visible.sync="openInfo" title="文章修改" top="2vw">
      <el-form :model="form" label-width="80px">
        <el-form-item label="活动名称">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item style="position: relative ;" label="知识内容">
          <Editor @child-event="handleData" v-if="form.contentInfo != ''" v-model="TxtValue" style="height: 11vw;">
          </Editor>
        </el-form-item>
        <el-form-item style="position: relative ;margin-top: 5vw;" label="选择类别">
          <el-select v-model="form.twType" placeholder="请选择类别">
            <el-option v-for="item in typeList" :key="item" :label="item" :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item style="position: relative;" label="相关图片">
          <el-upload action="http://127.0.0.1:10035/fileUpdate/upload" list-type="picture-card"
            :on-remove="handleRemove" :file-list="fileList" :multiple="true" :limit="9" :on-exceed="handleExceed"
            :before-upload="beforeUpload" :on-success="handleSuccess" :on-error="handleError">
            <i class="el-icon-plus"></i>
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
import { editInfo, getDocList, getInfo } from "@/api/kcInfo";
import { selectTw, selectById } from "@/api/login";
import Editor from "@/components/EditorUse.vue";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'TWInfo',
  components: {
    Editor,
    Foot, headInfo
  },
  data() {
    return {
      showPage: false,
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
      page: "图文认知",
      typeList: ["全部", "起降", "飞行", "通信载荷使用", "探测载荷使用", "攻击载荷使用"],
      contentList: [],
      selectName: "",
      twType: "",
      twType1: "全部",
      pageSize: 6,
      pageNum: 1,
      total: 0,
      totalPage: 0,
      pagesList: [],
      onePagesList: [],
      openInfo: false,


      form: {
        name: "",
        contentInfo: "",
        twType: "",
      },
      TxtValue: "",
      id: 0,
      fileList: [], // 已上传文件列表
      isUpload: 0,

      allImgs: "",
      contentListAll:[]
    }

  },
  methods: {
    handlePagination() {
      if (this.$route.query.id != null && this.$route.query.id != undefined) {
        console.log("dhsajdhjsagdhjasgdjhgas")
        this.pageSize = 6;
        this.total = this.contentListAll.length;
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
    handleData(data) {
      if (this.allImgs == "") {
        this.allImgs = this.allImgs + data
      } else {
        this.allImgs = this.allImgs + "," + data
      }

      console.log(data);  // 输出: "Data from Child"
    },
    goInfo(info) {
      console.log(info)
      this.$router.push('/' + info)
    },
    changeType(item) {
      this.twType1 = item;
      if (this.twType1 == "全部") {
        this.twType = "";
      } else {
        this.twType = this.twType1
      }
      this.pageNum = 1;
      this.getContentList();
    },

    getContentList() {
      var data = {
        name: this.selectName,
        twType: this.twType,
        pageNum: this.pageNum,
        pageSize: this.pageSize
      }
      // const id = this.$route.query.id;
      
      // if(id != null && id != undefined){
      //   var data1 = {
      //     id: id,
      //   }
      //   const res = await selectTw(data1)
      //   var l = res.data[0];
      //   console.log(l)
      //   var parentId = l.parentId;
      //   console.log(parentId)
      //   if(parentId != null && parentId != undefined){
      //     data.id = parentId;
      //   } 
      // }
      // console.log(data)
      getDocList(data).then((res) => {
        if (res.code != 500) {
          if (res.data.list != undefined) {
            console.log(res.data)
            this.contentList = res.data.list;
            this.total = res.data.total;
            this.totalPage = res.data.totalPages;
            for(let i = 0;i < this.contentList.length;i++){
              var c1 = this.contentList[i];
              c1.index = (this.pageNum - 1) * this.pageSize + i + 1;
            }
          }
        } else {
          if (res.msg == "token无效")
            localStorage.clear();
          this.$router.push('/')
        }
      })
    },
    goXq(id) {
      var data = {
        id: id
      }
      getInfo(data).then((res) => {
        this.$router.push({ path: '/TwInfoXq', query: { id: id, level: res.data.level, type: "tw" } })
      })
      localStorage.setItem("pageNum", this.pageNum)
    },

    editTw(id) {
      //展示出一个修改的弹窗
      var data = {
        id: id
      }
      this.allImgs = ""
      getInfo(data).then((res) => {
        this.openInfo = true;
        this.form.contentInfo = res.data.data.contentInfo
        this.form.name = res.data.data.name
        this.form.twType = res.data.data.twType
        this.TxtValue = res.data.data.contentInfo;
        this.id = id;
        var aaaaa = res.data.data.imgList;
        var imgs = [];
        for(let i = 0;i < aaaaa.length;i++){
          if(aaaaa[i].imgUrl !== ""){
            imgs.push(aaaaa[i]);
            break;
          }
        }
        // if(imgs.length == 0){
        //   imgs = [];
        // }
        console.log(imgs)
        this.fileList = [];
        for (let j = 0; j < imgs.length; j++) {
          var ii = {
            uuid: imgs[j].imgId,
            url: imgs[j].imgUrl
          }
          this.fileList.push(ii)
        }
        console.log(res);

      })

    },


    //照片墙
    // 处理图片移除
    handleRemove(file, fileList) {
      this.fileList = fileList;
      console.log('File removed:', file);
      console.log('Current fileList:', fileList);
    },
    // 当超过限制时触发
    handleExceed(files, fileList) {
      this.$message.warning(`当前限制选择 9 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
    },
    // 在上传前进行校验
    beforeUpload(file) {
      const isJPGorPNG = file.type === 'image/jpeg' || file.type === 'image/png';
      const isLt2M = file.size / 1024 / 1024 < 10; // 限制大小不超过2MB

      if (!isJPGorPNG) {
        this.$message.error('上传图片只能是 JPG/PNG 格式!');
      }
      if (!isLt2M) {
        this.$message.error('上传图片大小不能超过 2MB!');
      }
      return isJPGorPNG && isLt2M;
    },
    // 上传成功后的回调
    handleSuccess(response, file, fileList) {
      console.log('Upload success:', response);
      // 更新 fileList，确保新上传的文件被正确添加到列表中
      console.log(fileList)
      this.fileList = fileList;
      this.isUpload = 1;
    },
    // 上传失败后的回调
    // eslint-disable-next-line no-unused-vars
    handleError(err, file, fileList) {
      console.log('Upload error:', err);
      this.$message.error('上传失败，请重试！');
    },
    submitInfo() {

      var urlStr = "";
      for (let f = 0; f < this.fileList.length; f++) {
        if (f == 0) {
          if (this.fileList[f].response != null) {
            urlStr = this.fileList[f].response.data.url
          } else {
            urlStr = this.fileList[f].url
          }

        } else {
          if (this.fileList[f].response != null) {
            urlStr = urlStr + "," + this.fileList[f].response.data.url
          } else {
            urlStr = urlStr + "," + this.fileList[f].url
          }

        }
      }
      if (this.form.twType == "全部") {
        this.form.twType = "";
      }
      var data = {
        name: this.form.name,
        contentInfo: this.TxtValue,
        imgs: urlStr,
        id: this.id,
        type: 1,
        twType: this.form.twType,
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
      const id = this.$route.query.id;
      console.log(id)
      // const type = this.$route.query.type;
      if (id != null && id != undefined) {
        var data = {
          id: id,
        }
        selectTw(data).then(async (res) => {
          console.log(res.data)
          var list = res.data;
          var data1 = { list: list };
          var list1 = await selectById(data1);
          this.contentList = list1.data;
          this.contentList = this.contentList.filter((item, index, self) => {
            return index === self.findIndex((t) => t.id === item.id);
          });
          this.contentList.sort((a, b) => a.id - b.id);
          // this.onePagesList = [];
          // this.pagesList = [];
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
  padding-top: 1vw;

}

.oneRight {
  width: 98%;
  height: 4.6vw;
  line-height: 3vw;
  margin: 0 1%;
  display: flex;
  flex-direction: row;
  text-align: center;
  color: #ffffff;
  font-size: 1vw;
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
  position: absolute;
  top: 8%;
  left: 10%;
}

input {
  width: 96%;
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

el-pagination is-background .number {
  background-color: transparent !important;
}
</style>
