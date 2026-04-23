<template>
  <div style="width: 100%;height: 100%;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:-1;" src="../assets/img/twbg.png">
    <headInfo></headInfo>

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
                <div class="oneMuluXuan" v-if="item.name === '帮助文档'">
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
      <div class="rightContent">
        <div class="contentInfo" style="position: relative;">
          <div style="position: absolute;background-color: rgba(255,255,255,0.17);z-index: -1;width: 95%;height: 95%;left: 2.5%;border-radius: 2vw;"></div>
          <div class="word-viewer-container">
            <h1 style="text-align: center">{{ HelpName }}</h1>

            <div v-if="loading" class="loading">
              <p>正在加载文档...</p>
            </div>

            <div v-if="error" class="error">
              <p>{{ error }}</p>
            </div>

            <div v-if="document" class="document-view">
              <!-- 页面设置信息 -->

              <!-- 文档内容 -->
              <div class="document-content">
                <div v-for="(element, index) in document.elements" :key="index" class="document-element">
                  <!-- 段落 -->
                  <div v-if="element.type === 'paragraph'" class="paragraph"
                       :style="{
                 textAlign: element.alignment || 'left',
                 marginLeft: element.indentLeft ? element.indentLeft + 'px' : '0',
                 marginRight: element.indentRight ? element.indentRight + 'px' : '0',
                 textIndent: element.firstLineIndent ? element.firstLineIndent + 'px' : '0',
                 marginTop: element.spacingBefore ? element.spacingBefore + 'px' : '0',
                 marginBottom: element.spacingAfter ? element.spacingAfter + 'px' : '0',
                 lineHeight: '3vw'
               }">
            <span v-for="(run, runIndex) in element.content" :key="runIndex"
                  :style="{
                    lineHeight:'2vw',
                    fontWeight: run.bold ? 'bold' : 'normal',
                    fontStyle: run.italic ? 'italic' : 'normal',
                    textDecoration: run.underline ? 'underline' : 'none',
                    color: run.color || 'inherit',
                    fontSize: run.fontSize ? run.fontSize / 2 + 'pt' : 'inherit',
                    fontFamily: run.fontFamily || 'inherit'
                  }">
              {{ run.text }}
            </span>

                    <!-- 图片 -->
                    <div v-for="imgRun in element.content.filter(r => r.type === 'image')" :key="imgRun.images[0].id">
                      <img v-for="img in imgRun.images" :key="img.id"
                           :src="img.src"
                           :width="img.width"
                           style="display: block; max-width: 50%; height: auto;object-fit: contain;margin: 0 auto"/>
                    </div>
                  </div>

                  <!-- 表格 -->
                  <div v-if="element.type === 'table'" class="table-container">
                    <table :style="{
                   marginLeft: element.tableIndent ? element.tableIndent + 'px' : '0',
                   width: element.layout === 'fixed' ? 'auto' : '100%'
                 }">
                      <tr v-for="(row, rowIndex) in element.rows" :key="rowIndex"
                          :style="{ height: row.height ? row.height + 'px' : 'auto' }">
                        <td v-for="(cell, cellIndex) in row.cells" :key="cellIndex"
                            :style="{
                      width: cell.width ? cell.width + 'px' : 'auto',
                      paddingLeft: cell.marginLeft ? cell.marginLeft + 'px' : '8px',
                      paddingRight: cell.marginRight ? cell.marginRight + 'px' : '8px',
                      backgroundColor: cell.backgroundColor || 'transparent'
                    }">
                          <div v-for="(content, contentIndex) in cell.contents" :key="contentIndex">
                            <!-- 表格中的段落 -->
                            <div v-if="content.type === 'paragraph'" class="paragraph">
                      <div v-for="(run, runIndex) in content.content" :key="runIndex"
                            :style="{
                              fontWeight: run.bold ? 'bold' : 'normal',
                              fontStyle: run.italic ? 'italic' : 'normal',
                              textDecoration: run.underline ? 'underline' : 'none',
                              color: run.color || 'inherit',
                              fontSize: run.fontSize ? run.fontSize / 2 + 'pt' : 'inherit',
                              fontFamily: run.fontFamily || 'inherit'
                            }">
                        {{ run.text }}
                      </div>
                            </div>

                            <!-- 嵌套表格 -->
                            <div v-if="content.type === 'table'" class="nested-table">
                              <table>
                                <tr v-for="(nestedRow, nestedRowIndex) in content.rows" :key="nestedRowIndex">
                                  <td v-for="(nestedCell, nestedCellIndex) in nestedRow.cells" :key="nestedCellIndex">
                                    <div v-for="(nestedContent, nestedContentIndex) in nestedCell.contents"
                                         :key="nestedContentIndex">
                                      <!-- 嵌套表格中的内容 -->
                                    </div>
                                  </td>
                                </tr>
                              </table>
                            </div>
                          </div>
                        </td>
                      </tr>
                    </table>
                  </div>
                </div>
              </div>
            </div>

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
import {getHelpContent} from "@/api/kcInfo";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'TWInfoXq',
  components: {Foot, headInfo},
  data() {
    return {
      HelpName:"知识图谱操作使用手册",
      loading: false,
      error: null,
      document: null,
      filePath: null,
      url: "",
      userName: "",
      page: "帮助文档",
      mulu: [
        { id: 0, name: "知识图谱", info: "Graph" },
        { id: 1, name: "辅助决策", info: "BaoGao" },
        { id: 2, name: "图文资源", info: "TwInfo" },
        { id: 3, name: "视频资源", info: "SpInfo" },
        { id: 4, name: "动画显示", info: "DhInfo" },
        { id: 5, name: "数值计算", info: "JsInfo" },
        { id: 6, name: "帮助文档", info: "HelpInfo" }
      ],


    }
  },
  methods: {
    async loadDocument() {
      this.loading = true;
      this.error = null;
      this.document = null;
      var data = {
         id:this.docId
      }

      getHelpContent(data).then((res) => {
        this.document = res.data;
        this.loading = false;
      })


    },
    goInfo(info) {
      console.log(info)
      this.$router.push('/' + info)
    },
  },
  mounted() {
    this.docId = this.$route.query.id;
    this.userType = localStorage.getItem("type");
    this.userName = localStorage.getItem("name");
    this.loadDocument();
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

.contentInfo {
  width: 100%;
  height: 96%;
  position: absolute;
  z-index: 101;
  margin-top: 2%;
  border-radius: 1vw;
}

.word-viewer-container {
  max-width: 94%;
  margin: 0 auto;
  font-family: Arial, sans-serif;
  height: 95%;
  overflow-y: scroll;
  color: #FFFFFF;
  font-size: 1vw;
  padding: 0vw 2vw;
}
.word-viewer-container::-webkit-scrollbar {
  display: none;
}

</style>
