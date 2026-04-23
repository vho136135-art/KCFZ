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
              数值计算名称
            </div>
          </div>


          <div class="graphcontains2">
            <div class="custom-select" @click="toggleOptions1">
              <div style="font-size: 0.9vw;width: 4vw;color: #FFFFFF;line-height: 1.6vw">种类:</div>
              <div style="width: 10vw;position: relative;">
                <img src="../assets/img/graphInput.png" style="position: absolute;z-index: 99;width:100%;height: 100%;">
                <div class="selected-option">
                  {{ selectedOption1 ? selectedOption1 : '请选择类型' }}
                </div>
                <img src="../assets/img/graphDown.png"
                  style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                  v-if="typePic1 == 0">
                <img src="../assets/img/graphUp.png"
                  style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                  v-if="typePic1 == 1">
                <ul v-if="showOptions1" class="options">
                  <li v-for="(option, index) in options1" :key="index" @click="selectOption1(option)" class="option">
                    {{ option }}
                  </li>
                </ul>
              </div>
            </div>
          </div>


        </div>




        <div class="rightList">

          <div class="rightListContent" v-if="this.userType == 0">
            <div class="thumbnail-container" v-if="showQJFXT" @click="goXq(id1)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <img :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;object-fit: contain;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text1 }}</div>
              </div>
              <div class="preview">
                <img :src=src1 class="preview-image">
              </div>
              <!-- <div style="vertical-align: middle;align-items: center;display: flex;">
                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                  <el-image :src="require('@/assets/img/qianbiao.png')"
                    style="display: inline-block;width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;" />
                </div>
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text1 }}</div>
              </div> -->
              <!-- <div style="display: flex;justify-content: start;align-items: center;">
                <div style="color: #FFFFFF;">{{ text1 }}</div>
              </div> -->
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id1)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showDBDLC" @click="goXq(id2)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text2 }}</div>
              </div>
              <div class="preview">
                <img :src=src2 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id2)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showLDWLT" @click="goXq(id3)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text3 }}</div>
              </div>
              <div class="preview">
                <img :src=src3 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id3)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showSNJS" @click="goXq(id4)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text4 }}</div>
              </div>
              <div class="preview">
                <img :src=src4 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id4)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showSN1" @click="goXq(id5)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text5 }}</div>
              </div>
              <div class="preview">
                <img :src=src5 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id5)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showYLDQGJ" @click="goXq(id6)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text6 }}</div>
              </div>
              <div class="preview">
                <img :src=src6 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id6)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showDDZZSYFZJC" @click="goXq(id7)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text7 }}</div>
              </div>
              <div class="preview">
                <img :src=src7 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id7)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showDQJS" @click="goXq(id8)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text8 }}</div>
              </div>
              <div class="preview">
                <img :src=src8 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id8)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showCDBTX" @click="goXq(id9)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                            style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text9 }}</div>
              </div>
              <div class="preview">
                <img :src=src9 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id8)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div> -->
            </div>
            <!-- <div class="oneRight" v-for="item in contentList" :key="item">
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
            </div> -->
          </div>
          <div class="rightListContent" v-if="this.userType == 1">
            <div class="thumbnail-container" v-if="showQJFXT" @click="goXq(id1)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text1 }}</div>
              </div>
              <div class="preview">
                  <img :src=src1 class="preview-image">
                </div>
              <!-- <div style="display: flex;justify-content: start;align-items: center;">
                <div style="color: #FFFFFF;">{{ text1 }}</div>
              </div> -->
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id1)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id1)">修改</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showCDBTX" @click="goXq(id9)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
                
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text9 }}</div>
              </div>
              <div class="preview">
                <img :src=src9 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id8)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id8)">修改</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showLDWLT" @click="goXq(id3)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text3 }}</div>
              </div>
              <div class="preview">
                <img :src=src3 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id3)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id3)">修改</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showDBDLC" @click="goXq(id2)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text2 }}</div>
              </div>
              <div class="preview">
                <img :src=src2 class="preview-image">
              </div>
              <!-- <div style="display: flex;justify-content: start;align-items: center;">
                <div style="color: #FFFFFF;">{{ text2 }}</div>
              </div> -->
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id2)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id2)">修改</div>
              </div> -->
            </div>
            
            <div class="thumbnail-container" v-if="showSNJS" @click="goXq(id4)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text4 }}</div>
              </div>
              <div class="preview">
                <img :src=src4 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id4)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id4)">修改</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showSN1" @click="goXq(id5)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text5 }}</div>
              </div>
              <div class="preview">
                <img :src=src5 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id5)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id5)">修改</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showYLDQGJ" @click="goXq(id6)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text6 }}</div>
              </div>
              <div class="preview">
                <img :src=src6 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id6)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id6)">修改</div>
              </div> -->
            </div>
            
            <div class="thumbnail-container" v-if="showDQJS" @click="goXq(id8)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text8 }}</div>
              </div>
              <div class="preview">
                <img :src=src8 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id8)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id8)">修改</div>
              </div> -->
            </div>
            <div class="thumbnail-container" v-if="showDDZZSYFZJC" @click="goXq(id7)">
              <div style="vertical-align: middle;align-items: center;display: flex;">
<!--                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">-->
<!--                  <el-image :src="require('@/assets/img/qianbiao.png')"-->
<!--                    style="display: flex;width: 0.6vw;margin-left: 1vw;margin-right: 1.4vw;height: 100%;align-items: center;" />-->
<!--                </div>-->
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 1.2vw;margin-bottom:7%;">{{ text7 }}</div>
              </div>
              <div class="preview">
                <img :src=src7 class="preview-image">
              </div>
              <!-- <div
                style="width: 10%;text-decoration: underline;font-style: italic;position: relative;margin-left: 40%;display: flex;align-items: center;"
                @click="goXq(id7)">
                <img src="../assets/img/jsbutton.png" style="width: 6vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align: center;width: 6vw;height: 1.6vw;">查看详情</div>
              </div>
              <div
                style="width: 10%;text-decoration: underline;font-style: italic;display: flex;justify-content: space-around;position: relative;align-items: center;">
                <img src="../assets/img/jsbutton.png" style="width: 4vw;height: 1.6vw;">
                <div style="position: absolute;top: 0vw;text-align:center;width: 4vw;height: 1.6vw;"
                  @click="editJs(id7)">修改</div>
              </div> -->
            </div>



            
          </div>
          <div class="pageList">
            <page-info style="margin-left: 1vw;" v-if="showPage" :total="total" :page.sync="pageNum"
              :limit.sync="pageSize" @pagination="handlePagination()" />
          </div>
        </div>
      </div>
    </div>


    <div style="width: 100%;height: 3%;position: fixed;bottom: 0px;">
      <foot></foot>
    </div>


    <!--  数值计算详情修改  -->
    <el-dialog :visible.sync="openInfo" title="计算修改">
      <el-form :model="form" label-width="80px">
        <el-form-item label="计算名称">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="计算类型">
          <el-select v-model="form.jsType" placeholder="请选择动画类型">
            <el-option v-for="item in typeList" :key="item" :label="item" :value="item">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="计算地址">
          <el-input v-model="form.jsInfo" autocomplete="off"></el-input>
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
import { editInfo, getJsList, getInfo, getByParentIdAndType } from "@/api/kcInfo";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'JsInfo',
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
      page: "数值计算",
      typeList: ["全部", "起降", "飞行", "通信载荷使用", "探测载荷使用", "攻击载荷使用"],
      contentList: [],
      selectName: "",
      jsType: "",
      jsType1: "",
      pageSize: 4,
      pageNum: 1,
      total: 0,
      totalPage: 0,
      showPage:false,
      pagesList: [],
      onePagesList: [],
      openInfo: false,
      showQJFXT: false,
      showDBDLC: false,
      showLDWLT: false,
      showSNJS: false,
      showSN1: false,
      showYLDQGJ: false,
      showDDZZSYFZJC: false,
      showDQJS: false,
      showCDBTX: false,
      src1: require("@/assets/img/QJFXT.png"),
      src2: require("@/assets/img/DBDLC.png"),
      src3: require("@/assets/img/LDWLT.png"),
      src4: require("@/assets/img/SNJS.png"),
      src5: require("@/assets/img/SN1.png"),
      src6: require("@/assets/img/YLDQGJ.png"),
      src7: require("@/assets/img/DDZZSYFZJC.png"),
      src8: require("@/assets/img/DQJS.png"),
      src9: require("@/assets/img/CDBTX.png"),
      id1: 0,
      id2: 0,
      id3: 0,
      id4: 0,
      id5: 0,
      id6: 0,
      id7: 0,
      id8: 0,
      id9: 0,

      form: {
        name: "",
        jsType: "",
        jsInfo: "",
      },
      TxtValue: "",
      id: 0,
      fileList: [], // 已上传文件列表
      isUpload: 0,
      typePic1: 0,
      //下拉框
      showOptions1: false,
      selectedOption1: null,
      options1: ["全部", "起降", "飞行", "通信载荷使用", "探测载荷使用", "攻击载荷使用"],
      contentListAll:[]
    }

  },
  methods: {
    handlePagination() {
      if (this.$route.query.parentId != null && this.$route.query.parentId != undefined) {
        console.log("dhsajdhjsagdhjasgdjhgas")
        this.pageSize = 6;
        this.total = this.contentListAll.length;
        this.totalPage = Math.ceil(this.total / this.pageSize);
        console.log(this.contentListAll)
        
        const startIndex = (this.pageNum - 1) * this.pageSize;
        const endIndex = Math.min(startIndex + this.pageSize, this.contentListAll.length);

        // 获取当前页数据
        this.contentList = this.contentListAll.slice(startIndex, endIndex);
        console.log( this.contentList)


      } else {
        this.getContentList();
      }
    },
    selectOption1(option) {
      console.log(option)
      this.selectedOption1 = option;
      this.jsType1 = option;
      if (this.jsType1 == "全部") {
        this.jsType = "";
      } else {
        this.jsType = this.jsType1
      }
      this.getContentList();

      // this.showOptions1 = !this.showOptions1;
      // 触发事件，通知父组件当前选中的值

    },
    toggleOptions1() {
      if (this.typePic1 == 0) {
        this.typePic1 = 1;
      } else {
        this.typePic1 = 0
      }
      this.showOptions1 = !this.showOptions1;
    },
    goInfo(info) {
      console.log(info)
      this.$router.push('/' + info)
    },
    changeType(item) {
      this.jsType1 = item;
      if (this.jsType1 == "全部") {
        this.jsType = "";
      } else {
        this.jsType = this.jsType1
      }
      this.getContentList();
    },
    getContentList() {
      var data = {
        name: this.selectName,
        jsType: this.jsType,
        pageNum: this.pageNum,
        pageSize: this.pageSize
      }
      getJsList(data).then((res) => {
        console.log(data)
        if (res.code != 500) {
          if (res.data.list != undefined) {
            this.contentList = res.data.list;
            console.log(res.data.list)
            // for (let i = 0; i < this.contentList.length; i++) {
            //   const element = this.contentList[i];
            //   if (element.jsInfo == "QJFXT") {
            //     this.text1 = element.name;
            //     this.showQJFXT = true;
            //     this.id1 = element.id;
            //   } else if (element.jsInfo == "DBDLC") {
            //     this.text2 = element.name;
            //     this.showDBDLC = true;
            //     this.id2 = element.id;
            //   } else if (element.jsInfo == "LDWLT") {
            //     this.text3 = element.name;
            //     this.showLDWLT = true;
            //     this.id3 = element.id;
            //   } else if (element.jsInfo == "SNJS") {
            //     this.text4 = element.name;
            //     this.showSNJS = true;
            //     this.id4 = element.id;
            //   } else if (element.jsInfo == "SN1") {
            //     this.text5 = element.name;
            //     this.showSN1 = true;
            //     this.id5 = element.id;
            //   } else if (element.jsInfo == "YLDQGJ") {
            //     this.text6 = element.name;
            //     this.showYLDQGJ = true;
            //     this.id6 = element.id;
            //   } else if (element.jsInfo == "DDZZSYFZJC") {
            //     this.text7 = element.name;
            //     this.showDDZZSYFZJC = true;
            //     this.id7 = element.id;
            //   } else if (element.jsInfo == "DQJS") {
            //     this.text8 = element.name;
            //     this.showDQJS = true;
            //     this.id8 = element.id;
            //   }
            // }
            this.total = res.data.total;
            this.totalPage = res.data.totalPages;
            this.onePagesList = [];
            this.pagesList = [];
            this.updateOnePagesList();
          }
        } else {
          if (res.msg == "token无效")
            localStorage.clear();
          this.$router.push('/')
        }


      })
    },
    updateOnePagesList() {
      const startIndex = 0;
      // const endIndex = startIndex + this.pageSize;
      const endIndex = Math.min(startIndex + this.pageSize, startIndex + this.contentList.length)
      console.log(startIndex)
      console.log(endIndex)
      this.onePagesList = this.contentList.slice(startIndex, endIndex);
      this.text1 = this.text2 = this.text3 = this.text4 = this.text5 = this.text6 = this.text7 = this.text8 = this.text9 = '';
      this.showQJFXT = this.showDBDLC = this.showLDWLT = this.showSNJS = this.showSN1 = this.showYLDQGJ = this.showDDZZSYFZJC = this.showDQJS = this.showCDBTX = false;
      this.id1 = this.id2 = this.id3 = this.id4 = this.id5 = this.id6 = this.id7 = this.id8 = this.id9 = null;
      this.onePagesList.forEach((element) => {
        if (element.jsInfo == "QJFXT") {
          this.text1 = element.name;
          this.showQJFXT = true;
          this.id1 = element.id;
        } else if (element.jsInfo == "DBDLC") {
          this.text2 = element.name;
          this.showDBDLC = true;
          this.id2 = element.id;
        } else if (element.jsInfo == "LDWLT") {
          this.text3 = element.name;
          this.showLDWLT = true;
          this.id3 = element.id;
        } else if (element.jsInfo == "SNJS") {
          this.text4 = element.name;
          this.showSNJS = true;
          this.id4 = element.id;
        } else if (element.jsInfo == "SN1") {
          this.text5 = element.name;
          this.showSN1 = true;
          this.id5 = element.id;
        } else if (element.jsInfo == "YLDQGJ") {
          this.text6 = element.name;
          this.showYLDQGJ = true;
          this.id6 = element.id;
        } else if (element.jsInfo == "DDZZSYFZJC") {
          this.text7 = element.name;
          this.showDDZZSYFZJC = true;
          this.id7 = element.id;
        } else if (element.jsInfo == "DQJS") {
          this.text8 = element.name;
          this.showDQJS = true;
          this.id8 = element.id;
        }else if (element.jsInfo == "CDBTX") {
          this.text9 = element.name;
          this.showCDBTX = true;
          this.id9 = element.id;
        }

      });
    },
    goXq(id) {
      var data = {
        id: id
      }
      getInfo(data).then((res) => {
        console.log(res)
        this.$router.push({ path: '/JsInfoXq', query: { id: id, level: res.data.level, type: "js" } })
      })
      localStorage.setItem("pageNum",this.pageNum)
    },


    editJs(id) {
      //展示出一个修改的弹窗
      var data = {
        id: id
      }
      getInfo(data).then((res) => {

        this.openInfo = true;
        this.form.jsInfo = res.data.data.jsInfo
        this.form.name = res.data.data.name
        this.form.jsType = res.data.data.jsType;
        this.id = id;
        console.log(res);

      })

    },


    submitInfo() {
      console.log(this.fileList);


      var data = {
        id: this.id,
        type: 4,
        name: this.form.name,
        jsInfo: this.form.jsInfo,
        jsType: this.form.jsType,
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
          this.contentList = res.data.list;
          this.total = res.data.total;
          this.totalPage = res.data.totalPages;
          this.onePagesList = [];
          this.pagesList = [];
          this.updateOnePagesList();
          
          console.log(this.contentList)
        })
        this.contentListAll = this.contentList
        this.handlePagination();
      } else {
      this.getContentList();
      }
      localStorage.setItem("pageNum", 1)
    });
  },
  // watch: {
  //   pageNum(newVal, oldVal) {
  //     if (newVal !== oldVal) {
  //       this.getContentList();
  //     }
  //   }
  // }
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
  width: 100%;
  height: 78%;
  position: absolute;
  z-index: 2;
  margin-top: 9%;

  margin-bottom: 5%;
}

.rightListContent {
  width: 100%;
  height: 92%;
  position: absolute;
  z-index: 2;
  top: -3%;
  display: flex;
  flex-wrap: wrap
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

.password-input-container {
  width: 70%;
  height: 80%;
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

.custom-select {
  position: relative;
  width: 13.5vw;
  cursor: pointer;
  height: 70%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.selected-option {
  text-align: center;
  line-height: 1.8vw;
  width: 8vw;
  color: #FFFFFF;
}


.options {
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
}

.option {
  margin: 0.5vw;
  padding-left: 0.3vw;
  font-size: 0.7vw;
  color: #FFFFFF;

}

.option:hover {
  background-image: url("../assets/img/optionSelect.png");
  background-size: 100% 100%;
  color: #000000;

}

/*滚动条高宽度*/
.options::-webkit-scrollbar {
  width: 6px;
  height: 2px;
}

/*滚动条滑块*/
.options::-webkit-scrollbar-thumb {
  border-radius: 3px;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  background: #76ceff;
}

/*滚动条里面轨道*/
.options ::-webkit-scrollbar-track {
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.2) inset;

}

/*滚动条的小边角*/
.options::-webkit-scrollbar-corner {
  background: transparent;
}

.option {
  margin: 0.5vw;
  padding-left: 0.3vw;
  font-size: 0.7vw;

}

.graphcontains2 {

  height: 2.5vw;
  position: relative;
  display: flex;
  flex-direction: row;
  margin-top: 0.5vw;



}


.preview-image {
  object-fit: contain;
  height: 13vw;
  border: 2px solid #00f6ff;
  border-radius: 1vw;
  background-color: rgba(255, 255, 255, 0.44);
  box-shadow: 2px 3px 10px 4px #23f9fd80;
  cursor: pointer;
  }

.thumbnail-container {
  margin-bottom: 3%;
  width: 40%;
  height: 28vh;
  display: flex;
  margin-left: 4.8%;
  margin-right: 4.8%;
  flex-direction: column;
  align-items: center;


}

.biaotouqian /deep/ .el-image__inner {
  height: 15%;
  width: 100%;
}
</style>
