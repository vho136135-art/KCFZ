<template>
  <div style="width: 100%;height: 100%;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:-1;" src="../assets/img/graphbg.png">
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
      <div
        style="color: #ffffff; width: 62%;height:5vw;position: absolute;z-index: 1000;left: 12vw;top: 5.4vw;display: flex;flex-direction: row;justify-content: space-around;">
        <div class="graphcontains1">
          <div
            style="width: 100%;height: 1.6vw;position: relative;display: flex;flex-direction: row;justify-content: flex-start;margin-bottom: 0.5vw;">
            <div style="width: 6vw;display: flex;justify-content: flex-start;">
              <img src="../assets/img/juxing.png" style="width: 1.2vw;object-fit: contain;margin-right: 0.25vw;">
              <div style="height:1.6vw;line-height: 1.6vw;color: white;font-size: 1vw;font-size: 1vw; ">关键词：
              </div>
            </div>
            <div style="width:10vw;height: 1.7vw;position: relative;">
              <img src="../assets/img/graphInput.png" style="position: absolute;z-index: 99;width:100%;height: 100%;">
              <input type="text" placeholder="请输入关键词" v-model="keywords" @keyup.enter="getInfo1()" />
              <div style="width: 10%;height: 0.8vw;position: absolute;right: 0.5vw;z-index: 5555;top: 0.3vw;"
                @click="getInfo1()">
                <img src="../assets/img/look.png" style="width: 100%;height: 100%;">
              </div>
            </div>
          </div>
        </div>

        <div class="graphcontains2">
          <div class="custom-select" @click="toggleOptions2">
            <div style="font-size: 1vw;width: 6vw;">飞机任务:</div>
            <div style="width: 10vw;position: relative;">
              <img src="../assets/img/graphInput.png" style="position: absolute;z-index: 99;width:100%;height: 100%;">

              <div class="selected-option">
                {{ selectedOption2 ? selectedOption2.text : '请选择任务' }}
              </div>
              <img src="../assets/img/graphDown.png"
                style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                v-if="typePic2 == 0">
              <img src="../assets/img/graphUp.png"
                style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                v-if="typePic2 == 1">
              <ul v-if="showOptions2" class="options">
                <li v-for="(option, index) in options2" :key="index" @click="selectOption2(option)" class="option">
                  {{ option.label }}
                </li>
              </ul>
            </div>

          </div>
        </div>
        <div class="graphcontains2">
          <div class="custom-select" @click="toggleOptions1">
            <div style="font-size: 1vw;width: 6vw;">飞机类型:</div>
            <div style="width: 10vw;position: relative;">
              <img src="../assets/img/graphInput.png" style="position: absolute;z-index: 99;width:100%;height: 100%;">
              <div class="selected-option">
                {{ selectedOption1 ? selectedOption1.text : '请选择类型' }}
              </div>
              <img src="../assets/img/graphDown.png"
                style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                v-if="typePic1 == 0">
              <img src="../assets/img/graphUp.png"
                style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                v-if="typePic1 == 1">
              <ul v-if="showOptions1" class="options">
                <li v-for="(option, index) in options1" :key="index" @click="selectOption1(option)" class="option">
                  {{ option.label }}
                </li>
              </ul>
            </div>
          </div>
        </div>
        <!-- // -->
        <div class="graphcontains2">
          <div class="custom-select" @click="toggleOptions3">
            <div style="font-size: 1vw;width: 6vw;">飞机载荷:</div>
            <div style="width: 10vw;position: relative;">
              <img src="../assets/img/graphInput.png" style="position: absolute;z-index: 99;width:100%;height: 100%;">

              <div class="selected-option">
                {{ selectedOption3 ? selectedOption3.text : '请选择载荷' }}
              </div>
              <img src="../assets/img/graphDown.png"
                style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                v-if="typePic3 == 0">
              <img src="../assets/img/graphUp.png"
                style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                v-if="typePic3 == 1">
            </div>

          </div>
          <ul class="level-1" v-if="showOptions3">
            <li v-for="(item, index) in items" :key="'level1-' + index">
              <!-- 第一层 - 不可选，仅作为分类 -->
              <div class="parent-item" @click="toggleExpand(index)">
                <span class="arrow" :class="{ expanded: item.expanded }">▶</span>
                {{ item.label }}
              </div>

              <!-- 第二层 - 可选 -->
              <ul class="level-2" v-show="item.expanded" style="margin-left: 1vw;">
                <li v-for="(subItem, subIndex) in item.children" :key="'level2-' + subIndex">
                  <label style="font-size: 0.8vw;">
                    <input style="position: relative;width: 1vw;" type="checkbox" v-model="subItem.selected"
                      @change="handleSelect(subItem)">
                    {{ subItem.label }}
                  </label>
                </li>
              </ul>
            </li>
          </ul>
        </div>
        <div
          style="width: 10vw;background-color: #00f6ff;height: 1.7vw;line-height: 1.7vw;border-radius: 1vw;text-align: center;margin-left: 1vw;"
          @click="sumbitChoose()">查询
        </div>


      </div>
      <div
        style="width: 24%;display: flex;flex-direction: row;position: absolute;height: 1.7vw;right: 2vw;z-index: 2000;justify-content: space-around;margin-top: 1%;">
        <div style="width:21%;" v-if="userType == 1">
          <div
            style="height: 1.7vw;width: 100%;background-color: transparent;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0vw 0.1vw;border: 1px #2ed0d6 solid;justify-items: center;align-items: center;"
            @click="openFileInputData">
            <img src="../assets/img/Inicon.png" style="height: 60%;object-fit: contain;">
            <div style="color: #FFFFFF;margin-left: 0.25vw;font-size: 0.9vw;">导入资源</div>
          </div>
          <input ref="fileInputData" type="file" accept=".doc, .docx" style="display: none;"
            @change="handleFileChangeData" />

        </div>
        <div style="width:21%;" v-if="userType == 1">
          <div
            style="height: 1.7vw;width: 100%;background-color: transparent;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0vw 0.1vw;border: 1px #2ed0d6 solid;justify-items: center;align-items: center;"
            @click="openEditBao">
            <img src="../assets/img/Inicon.png" style="height: 60%;object-fit: contain;">
            <div style="color: #FFFFFF;margin-left: 0.25vw;font-size: 0.9vw;">资源文件</div>
          </div>

        </div>
        <div style="width:20%;" v-if="userType == 1" @click="exportAllContent">
          <div
            style="height: 1.7vw;width: 100%;background-color: transparent;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0vw 0.1vw;border: 1px #2ed0d6 solid;justify-items: center;align-items: center;">
            <div style="color: #FFFFFF;margin-left: 0.25vw;font-size: 0.9vw;">导出</div>
          </div>
        </div>
        <div style="width:20%;" v-if="userType == 1">
          <div
            style="height: 1.7vw;width: 100%;background-color: transparent;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0vw 0.1vw;border: 1px #2ed0d6 solid;justify-items: center;align-items: center;"
            @click="openFileInput">
            <img src="../assets/img/Inicon.png" style="height: 60%;object-fit: contain;">
            <div style="color: #FFFFFF;margin-left: 0.25vw;font-size: 0.9vw;">导入</div>
          </div>
          <input ref="fileInput" type="file" accept=".doc, .docx" style="display: none;" @change="handleFileChange" />


        </div>


      </div>

      <div class="rightContent">
        <div class="rightList">
          <div class="tupu">
            <div style="width: 100%;height: 100%;">
              <div class="gContainer">
                <RelationGraph ref="graphRef" :options="graphOptions" :on-node-expand="onNodeExpand"
                  :on-line-collapse="onNodeCollapse">
                  <template #node="{ node }">
                    <div v-if="node.data.type == 0 && node.data.group == '1'" style="font-size: 2vw;padding-top: 40%;"
                      @dblclick="showPopup(node)">
                      {{ node.text }}
                    </div>
                    <div v-if="node.data.type == 0 && node.data.group == '2'" style="font-size: 1.8vw;padding-top: 40%;"
                      @dblclick="showPopup(node)">
                      {{ node.text }}
                    </div>
                    <div v-if="node.data.type == 0 && node.data.group == '3'" style="font-size: 1.8vw;padding-top: 40%;"
                      @dblclick="showPopup(node)">
                      {{ node.text }}
                    </div>
                    <div v-if="node.data.type == 0 && node.data.group == '4'" style="font-size: 1.8vw;padding-top: 40%;"
                      @dblclick="showPopup(node)">
                      {{ node.text }}
                    </div>
                    <div v-if="node.data.type == 0 && node.data.group == '5'" style="font-size: 1.8vw;padding-top: 40%;"
                      @dblclick="showPopup(node)">
                      {{ node.text }}
                    </div>
                    <div v-if="node.data.type == 0 && node.data.group == '6'" style="font-size: 1.8vw;padding-top: 40%;"
                      @dblclick="showPopup(node)">
                      {{ node.text }}
                    </div>
                    <div v-if="node.data.type == 0 && node.data.group == '7'" style="font-size: 1.8vw;padding-top: 40%;"
                      @dblclick="showPopup(node)">
                      {{ node.text }}
                    </div>


                    <div v-if="node.data.type == 1 && node.data.group == '1'"
                         style="font-size: 1.5vw;height: 100%;width: 100%;display: flex;justify-content: center;justify-items: center;"
                         @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <div style="height: 5%;margin-top: 40%;">{{ node.text }}</div>
                    </div>
                    <div v-if="node.data.type == 1 && node.data.group == '2'"
                         style="font-size: 1.5vw;height: 100%;width: 100%;display: flex;justify-content: center;justify-items: center;"
                         @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <div style="height: 5%;margin-top: 40%;">{{ node.text }}</div>
                    </div>
                    <div v-if="node.data.type == 1 && node.data.group == '3'"
                         style="font-size: 1.5vw;height: 100%;width: 100%;display: flex;justify-content: center;justify-items: center;"
                         @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <div style="height: 5%;margin-top: 40%;">{{ node.text }}</div>
                    </div>
                    <div v-if="node.data.type == 1 && node.data.group == '4'"
                         style="font-size: 1.5vw;height: 100%;width: 100%;display: flex;justify-content: center;justify-items: center;"
                         @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <div style="height: 5%;margin-top: 40%;">{{ node.text }}</div>
                    </div>
                    <div v-if="node.data.type == 1 && node.data.group == '5'"
                         style="font-size: 1.5vw;height: 100%;width: 100%;display: flex;justify-content: center;justify-items: center;"
                         @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <div style="height: 5%;margin-top: 40%;">{{ node.text }}</div>
                    </div>
                    <div v-if="node.data.type == 1 && node.data.group == '6'"
                         style="font-size: 1.5vw;height: 100%;width: 100%;display: flex;justify-content: center;justify-items: center;"
                         @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <div style="height: 5%;margin-top: 40%;">{{ node.text }}</div>
                    </div>
                    <div v-if="node.data.type == 1 && node.data.group == '7'"
                         style="font-size: 1.5vw;height: 100%;width: 100%;display: flex;justify-content: center;justify-items: center;"
                         @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <div style="height: 5%;margin-top: 40%;">{{ node.text }}</div>
                    </div>


                    <div v-if="node.data.type == 2" @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <img src="http://127.0.0.1:10035/profile/videoPic.png" style="width: 100%;height: 100%">
                    </div>
                    <div v-if="node.data.type == 3" @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <img src="http://127.0.0.1:10035/profile/dhvideoPic.png" style="width: 100%;height: 100%">
                    </div>
                    <div v-if="node.data.type == 4" @dblclick="showPopup(node)" @mousedown="handleDrag(node)" @mousemove="handleMove()"
                         @mouseup="endDrag" @mouseleave="endDrag">
                      <img src="http://127.0.0.1:10035/profile/jsq.png" style="width: 100%;height: 100%">
                    </div>
                  </template>
                </RelationGraph>

              </div>
            </div>
          </div>
          <!-- 操作弹窗 -->
          <el-dialog title="操作分支内容" :visible.sync="isModalVisible" append-to-body top="10vh"
            custom-class="custom-dialog">

            <el-form label-width="90px">
              <el-form-item label="节点名称">
                <el-input v-model="nodeInfo.name" readonly></el-input>
              </el-form-item>
              <el-form-item label="节点层级">
                <el-input v-model="nodeInfo.group" readonly></el-input>
              </el-form-item>
              <el-form-item label="操作">
                <el-button type="primary" @click="openAdd()">新增下级</el-button>
                <el-button type="warning" @click="openEdit()">修改</el-button>
                <el-button type="danger" @click="deleteTw()">删除</el-button>
              </el-form-item>
            </el-form>
          </el-dialog>


          <!--     新增分支弹窗     -->
          <el-dialog title="添加分支内容" :visible.sync="isModalVisible1" append-to-body top="4vh"
            custom-class="custom-dialog">
            <el-form label-width="90px">
              <el-form-item label="fileId">
                <el-input v-model="newBranchFileId"></el-input>
              </el-form-item>
              <el-form-item label="类型">
                <el-select v-model="typeValue" placeholder="请选择类型">
                  <el-option label="图文" value="tw"></el-option>
                  <el-option label="视频" value="sp"></el-option>
                  <el-option label="动画" value="dh"></el-option>
                  <el-option label="计算模块" value="js"></el-option>
                </el-select>
              </el-form-item>

              <el-form-item style="position: relative ;" label="图文类别" v-if="this.typeValue == 'tw'">
                <el-select v-model="addTwType" placeholder="请选择类别">
                  <el-option v-for="item in twTypeList" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item style="position: relative ;" label="视频类别" v-if="this.typeValue == 'sp'">
                <el-select v-model="addSpType" placeholder="请选择类别">
                  <el-option v-for="item in otherTypeList" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item style="position: relative ;" label="动画类别" v-if="this.typeValue == 'dh'">
                <el-select v-model="addDhType" placeholder="请选择类别">
                  <el-option v-for="item in otherTypeList" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item style="position: relative ;" label="计算类别" v-if="this.typeValue == 'js'">
                <el-select v-model="addJsType" placeholder="请选择类别">
                  <el-option v-for="item in otherTypeList" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </el-form-item>


              <el-form-item label="节点名称">
                <el-input v-model="newBranchContent"></el-input>
              </el-form-item>
              <el-form-item label="计算模块地址" v-if="this.typeValue == 'js'">
                <el-input v-model="addJsInfo"></el-input>
              </el-form-item>

              <el-form-item style="position: relative ;" label="节点内容" v-if="this.typeValue == 'tw'">
                <Editor v-model="newBranchValue" style="height: 10vw;margin-bottom: 5vw;"></Editor>
              </el-form-item>

              <el-form-item style="position: relative;" label="相关图片" v-if="this.typeValue == 'tw'">
                <el-upload action="http://127.0.0.1:10035/fileUpdate/upload" list-type="picture-card"
                  :on-remove="handleRemove" :file-list="fileList" :multiple="true" :limit="9" :on-exceed="handleExceed"
                  :before-upload="beforeUpload" :on-success="handleSuccess" :on-error="handleError">
                  <i class="el-icon-plus"></i>
                </el-upload>
              </el-form-item>


              <el-form-item label="上传视频" prop="spUrl" v-if="this.typeValue == 'sp' || this.typeValue == 'dh'">
                <el-upload class="avatar-uploader el-upload--text" multiple :headers="videoUpload.headers"
                  :action="videoUpload.url" :file-list="videoFileList" :show-file-list="false" accept=".mp4"
                  :on-success="handleVideoSuccess" :before-upload="beforeUploadVideo" :on-progress="uploadVideoProcess"
                  :on-remove="handleVideoRemove">
                  <div v-if="!videoFlag && showVideoPath" style="display: flex; flex-wrap: wrap; gap: 10px;">
                    <!--                    <div v-for="(url, index) in showVideoPath.split(',')" :key="url"-->
                    <!--                         style="position: relative; flex: 1 1 calc(33.333% - 20px); min-width: 200px; margin-bottom: 10px;">-->
                    <video :src="showVideoPath" style="width:50%; height: auto;border-radius: 0.5vw;"
                      class="avatar video-avatar" controls>
                      您的浏览器不支持视频播放
                    </video>
                    <img src="../assets/img/delete.png" @click.stop="handleVideoRemove(videoFileList[0])"
                      style="width: 35px; height: 35px;position: absolute; top: 5px; left: 5px; cursor: pointer; z-index: 999;"
                      alt="删除" />
                    <!--                    </div>-->
                  </div>
                  <el-progress :stroke-width="10" class="progressType" v-if="videoFlag" type="circle"
                    :percentage="videoUploadPercent" style="margin-top:30px;"></el-progress>
                  <el-button style="z-index: 999;" class="video-btn" slot="trigger" size="small" type="primary">
                    点击上传视频
                  </el-button>
                </el-upload>
              </el-form-item>


              <!--              <el-form-item label="飞机类型" v-if="this.typeValue=='dh'">-->
              <!--                <el-select v-model="dhParam.fjlx" placeholder="请选择飞机类型">-->
              <!--                  <el-option label="直9" value="直9"></el-option>-->
              <!--                  <el-option label="直9-C" value="直9-C"></el-option>-->
              <!--                  <el-option label="卡式机" value="卡式机"></el-option>-->
              <!--                </el-select>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="飞机任务" v-if="this.typeValue=='dh'">-->
              <!--                <el-select v-model="dhParam.rwlx" placeholder="请选择任务类型">-->
              <!--                  <el-option label="侦察" value="侦察"></el-option>-->
              <!--                  <el-option label="巡逻" value="巡逻"></el-option>-->
              <!--                  <el-option label="作战" value="作战"></el-option>-->
              <!--                </el-select>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="飞机载荷" v-if="this.typeValue=='dh'">-->
              <!--                <el-select v-model="dhParam.zhlx" placeholder="请选择载荷类型">-->
              <!--                  <el-option label="鱼雷" value="鱼雷"></el-option>-->
              <!--                  <el-option label="侦察设备" value="侦察设备"></el-option>-->
              <!--                  <el-option label="导弹" value="导弹"></el-option>-->
              <!--                </el-select>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="风速"  v-if="this.typeValue=='dh'">-->
              <!--                <el-input v-model="dhParam.fs"></el-input>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="能见度"  v-if="this.typeValue=='dh'">-->
              <!--                <el-input v-model="dhParam.njd"></el-input>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="湿度"  v-if="this.typeValue=='dh'">-->
              <!--                <el-input v-model="dhParam.sd"></el-input>-->
              <!--              </el-form-item>-->


              <el-form-item label="父级节点ID" style="margin-top: 4vw;">
                <el-input v-model="newBranchParentId" disabled></el-input>
              </el-form-item>
              <el-form-item label="关系">
                <el-input v-model="newBranchRelation"
                  @input="newBranchRelation = $event.target.value.replace(/[^a-zA-Z\u4e00-\u9fa5]/g, '')"></el-input>
              </el-form-item>
              <el-form-item label="层级">
                <el-input-number v-model="newBranchLevel" controls-position="right" :min="1"></el-input-number>
              </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
              <el-button @click="closeModal">取 消</el-button>
              <el-button type="primary" @click="addNewBranch">提 交</el-button>
            </span>
          </el-dialog>


          <!--     修改分支弹窗     -->
          <el-dialog title="修改分支内容" :visible.sync="isModalVisible2" append-to-body top="1vh" style="height: 55vw;"
            custom-class="custom-dialog">
            <el-form label-width="90px">
              <el-form-item label="fileId">
                <el-input v-model="editFileId"></el-input>
              </el-form-item>
              <el-form-item label="类型">
                <el-select v-model="editType" placeholder="请选择类型">
                  <el-option label="图文" value="tw"></el-option>
                  <el-option label="视频" value="sp"></el-option>
                  <el-option label="动画" value="dh"></el-option>
                  <el-option label="计算模块" value="js"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="节点名称">
                <el-input v-model="editName"></el-input>
              </el-form-item>

              <!--      图文类型        -->
              <el-form-item style="position: relative ;" label="图文类别" v-if="this.editType == 'tw'">
                <el-select v-model="editTwType" placeholder="请选择图文类别">
                  <el-option v-for="item in twTypeList" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </el-form-item>


              <el-form-item style="position: relative ;" label="视频类别" v-if="this.editType == 'sp'">
                <el-select v-model="editSpType" placeholder="请选择视频类别">
                  <el-option v-for="item in otherTypeList" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </el-form-item>


              <el-form-item style="position: relative ;" label="动画类别" v-if="this.editType == 'dh'">
                <el-select v-model="editDhType" placeholder="请选择类别">
                  <el-option v-for="item in otherTypeList" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </el-form-item>

              <el-form-item style="position: relative ;" label="计算模块类别" v-if="this.editType == 'js'">
                <el-select v-model="editJsType" placeholder="请选择类别">
                  <el-option v-for="item in otherTypeList" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </el-form-item>


              <el-form-item label="计算模块地址" v-if="this.editType == 'js'">
                <el-input v-model="editJsInfo"></el-input>
              </el-form-item>


              <!--              <el-form-item label="飞机类型" v-if="this.editType=='dh'">-->
              <!--                <el-select v-model="editDhParam.fjlx" placeholder="请选择飞机类型">-->
              <!--                  <el-option label="直9" value="直9"></el-option>-->
              <!--                  <el-option label="直9-C" value="直9-C"></el-option>-->
              <!--                  <el-option label="卡式机" value="卡式机"></el-option>-->
              <!--                </el-select>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="飞机任务" v-if="this.editType=='dh'">-->
              <!--                <el-select v-model="editDhParam.rwlx" placeholder="请选择任务类型">-->
              <!--                  <el-option label="侦察" value="侦察"></el-option>-->
              <!--                  <el-option label="巡逻" value="巡逻"></el-option>-->
              <!--                  <el-option label="作战" value="作战"></el-option>-->
              <!--                </el-select>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="飞机载荷" v-if="this.editType=='dh'">-->
              <!--                <el-select v-model="editDhParam.zhlx" placeholder="请选择载荷类型">-->
              <!--                  <el-option label="鱼雷" value="鱼雷"></el-option>-->
              <!--                  <el-option label="侦察设备" value="侦察设备"></el-option>-->
              <!--                  <el-option label="导弹" value="导弹"></el-option>-->
              <!--                </el-select>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="风速"  v-if="this.editType=='dh'">-->
              <!--                <el-input v-model="editDhParam.fs"></el-input>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="能见度"  v-if="this.editType=='dh'">-->
              <!--                <el-input v-model="editDhParam.njd"></el-input>-->
              <!--              </el-form-item>-->
              <!--              <el-form-item label="湿度"  v-if="this.editType=='dh'">-->
              <!--                <el-input v-model="editDhParam.sd"></el-input>-->
              <!--              </el-form-item>-->

              <el-form-item style="position: relative ;margin-bottom: 5vw;" label="节点内容" v-if="this.editType == 'tw'">
                <Editor :key="forceUpdateKey"   v-model="editContent" style="height: 6vw;"></Editor>
              </el-form-item>
              <el-form-item label="父级节点ID">
                <el-input v-model="editParentId" disabled></el-input>
              </el-form-item>
              <el-form-item label="关系">
                <el-input v-model="editRelation"
                  @input="editRelation = $event.target.value.replace(/[^a-zA-Z\u4e00-\u9fa5]/g, '')"></el-input>
              </el-form-item>
              <el-form-item label="层级">
                <el-input-number v-model="editLeve" controls-position="right" :min="1"></el-input-number>
              </el-form-item>
              <el-form-item style="position: relative;" label="相关图片" v-if="this.editType == 'tw'">
                <el-upload action="http://127.0.0.1:10035/fileUpdate/upload" list-type="picture-card"
                  :on-remove="handleRemove" :file-list="fileList" :multiple="true" :limit="9" :on-exceed="handleExceed"
                  :before-upload="beforeUpload" :on-success="handleSuccess" :on-error="handleError">
                  <i class="el-icon-plus"></i>
                </el-upload>
              </el-form-item>

              <el-form-item label="上传视频" prop="spUrl" v-if="this.editType == 'sp' || this.editType == 'dh'">
                <el-upload class="avatar-uploader el-upload--text" multiple :headers="videoUpload.headers"
                  :action="videoUpload.url" :file-list="videoFileList" :show-file-list="false" accept=".mp4"
                  :on-success="handleVideoSuccess" :before-upload="beforeUploadVideo" :on-progress="uploadVideoProcess"
                  :on-remove="handleVideoRemove">

                  <div v-if="!videoFlag && showVideoPath" style="display: flex; flex-wrap: wrap; gap: 10px;">
                    <div
                      style="position: relative; flex: 1 1 calc(33.333% - 20px); min-width: 200px; margin-bottom: 10px;">

                      <video :src="showVideoPath" style="width:50%; height: auto;border-radius: 0.5vw;"
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
                  <el-button style="z-index: 999;" class="video-btn" slot="trigger" size="small" type="primary">
                    点击上传视频
                  </el-button>
                </el-upload>
              </el-form-item>


            </el-form>
            <span slot="footer" class="dialog-footer">
              <el-button @click="closeModal1">取 消</el-button>
              <el-button type="primary" @click="editSubmit">提 交</el-button>
            </span>
          </el-dialog>
        </div>

      </div>


    </div>
    <!--    v-if="shengOpen"-->
    <div style="width: 100%;height: 100%;position: absolute;background-color: rgba(0,0,0,0.58);z-index: 2000;top: 0vw;"
      v-if="shengOpen">
      <img src="../assets/img/baoGaoClose.png"
        style="width: 2vw;height: auto;object-fit: contain;position: absolute;top: 18%;right: 23%;z-index: 6000;"
        @click="shengOpen = false">
      <div class="bgBao">
        <img src="../assets/img/baoGaobg.png" style="height: 100%;object-fit: contain;position: absolute;z-index: -5;">

        <div
          style="width: 2vw;height: 7vw;background-color: transparent;position: absolute;top: 10%;left: 1.8%;display: flex;flex-direction: column;justify-content: center;">
          <img src="../assets/img/baoGaoEdit.png"
            style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit == 0"
            @click="openEditBao()">
          <img src="../assets/img/baoGaoDown.png"
            style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit == 0"
            @click="downLoadWord()">
          <img src="../assets/img/history.png" style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;"
            @click="openHistory" v-if="clickEdit == 0">

          <img src="../assets/img/baoGaoEdit1.png"
            style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit == 1">
          <img src="../assets/img/baoGaoDown.png"
            style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit == 1"
            @click="downLoadWord()">
          <img src="../assets/img/history.png" style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;"
            @click="openHistory" v-if="clickEdit == 1">


          <img src="../assets/img/baoGaoEdit.png"
            style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit == 2"
            @click="openEditBao()">
          <img src="../assets/img/baoGaoDown1.png"
            style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit == 2">
          <img src="../assets/img/history.png" style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;"
            @click="openHistory" v-if="clickEdit == 2">


          <img src="../assets/img/baoGaoEdit.png"
            style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit == 3"
            @click="openEditBao()">
          <img src="../assets/img/baoGaoDown.png"
            style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" @click="downLoadWord()"
            v-if="clickEdit == 3">
          <img src="../assets/img/history1.png" style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;"
            v-if="clickEdit == 3">
        </div>

        <div style="font-weight: 500;width: 35%;height: 4.5vw;background-color: transparent;
            margin-top: 0.2vw;margin-left: 5%;display: flex;flex-direction: row;justify-content: center;">

          <img src="../assets/img/baoJian.png"
            style="height: 1.2vw;object-fit: contain;margin-top: 1.65vw;margin-right: 10%;">
          <div style="line-height: 4.5vw;font-size: 1.5vw;color: #00f6ff;">
            报告
          </div>


        </div>
        <div class="baoGaoContentInfo"
          style="width: 85%;height: 76%;background-color: transparent;margin-left: 6%;margin-top: 0.5vw;padding: 0 2vw;overflow-y: scroll;">
          <div v-if="clickEdit != 3" class="baoGaoInfotest" style="line-height: 2vw;color: #ffffff;" v-html="baoContent"
            :key="this.editBaoGao"></div>


          <el-table v-else :data="tableData" style="width: 90%;margin-top: 2vw;margin-left: 5%;">
            <el-table-column prop="bgName" label="报告名称" header-align="center" align="center">
            </el-table-column>
            <el-table-column prop="name" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" @click="lookInfo(scope.row)">编辑
                </el-button>
                <el-button size="mini" type="warning" @click="downLoadInfo(scope.row)">下载
                </el-button>
                <el-button size="mini" type="danger" @click="delteInfo(scope.row)">删除
                </el-button>
              </template>
            </el-table-column>
            <!--            <el-table-column-->
            <!--                prop="address"-->
            <!--                label="地址">-->
            <!--            </el-table-column>-->
          </el-table>
        </div>

      </div>
    </div>
    <el-dialog title="上传视频，动画以及计算" :visible.sync="centerDialogVisible" width="30%" center>
      <el-upload class="upload-demo" action="http://127.0.0.1:10035/file/uploadAndExecuteSqls"
        :on-remove="handleRemoveSql" :before-remove="beforeRemoveSql" multiple :limit="3" :on-exceed="handleExceedSql"
        :file-list="fileListSql">
        <el-button size="small" type="primary">点击上传</el-button>

      </el-upload>
      <span slot="footer" class="dialog-footer">
        <el-button @click="centerDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>

    <!--     新增分支弹窗     -->
    <el-dialog title="上传资源" :visible.sync="editBaoGao" append-to-body top="4vh">
      <div style="display: flex;">
        <div style="margin-left: 1vw;width:20%;">
          <div
            style="height: 100%;width: 50%;background-color:#2ed0d6 ;border-radius: 0.3vw;display: flex;flex-direction: row;justify-content: center;border: 1px #2ed0d6 solid;"
            @click="openFileInputData11">
            <div style="line-height: 2.5vw;color: #FFFFFF;margin-left: 0.25vw;">选取文件</div>
          </div>
          <input ref="fileInputData11" type="file" accept=".doc, .docx" style="display: none;"
            @change="handleFileUpload" />

        </div>
        <el-button type="success" @click="uploadFileZip">上传</el-button>
      </div>


    </el-dialog>


    <el-dialog title="报告名称" :visible.sync="dialogVisibleInput" width="30%">
      <el-input v-model="baoGaoName" placeholder="请输入报告名称" style="margin-bottom: 1vw;"></el-input>
      <el-button @click="dialogVisibleInput = false">取 消</el-button>
      <el-button type="primary" @click="inputName">确 定</el-button>

    </el-dialog>


    <div style="width: 100%;height: 3%;position: fixed;bottom: 0px;">
      <foot></foot>
    </div>
  </div>

</template>
<script>
import headInfo from '@/components/Head.vue';
import Foot from "@/components/Foot.vue";
import { editInfoGraph, getInfo } from "@/api/kcInfo";
import { getDomainGraphNew, createNodeAndRelationship, getgraphInfo } from "@/api/login";
import { config } from '@/assets/defaultConfig.js'
import { addFile, addNode, getFileIdByDocId, uploadAndExecuteSql } from "@/api/file";
import Editor from "@/components/EditorUse.vue";
import { getToken } from "@/utils/auth";
import { twdelete } from "@/api/twdelete";
import { downLoadBaoGao, getAllHistory, insertBaoGao } from "@/api/baogao";
import { exportAll, getFileId, getFileIdData } from "@/api/export";
// , exportToWord,

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Graph',
  components: { Editor, Foot, headInfo },
  computed: {
    selectedItems() {
      return this.items
        .flatMap(item => item.children)
        .filter(child => child.selected);
    }
  },
  data() {
    return {
      openLevel: 7,
      graphOptions: {
        debug: false,
        lineUseTextPath: true,
        layout: {
          label: '树',
          layoutName: 'tree',
          layoutClassName: 'seeks-layout-center',
          from: 'top',
          // 通过这4个属性来调整 tree-层级距离&节点距离

          levelDistance: 200,      // 层与层之间的垂直间距
          nodeDistance: 150,       // 同一层级的水平间距
          min_per_width: 120,      // 最小水平间距（固定值）
          max_per_width: 120,      // 最大水平间距（固定值，强制均匀分布）
          min_per_height: 300,     // 最小垂直间距（固定值）
          max_per_height: 300,     // 最大垂直间距（固定值，强制对齐）
          disableDrag: true,       // 禁止拖动节点（可选）
          align: 'center',         // 居中排列
          fixed: false,            // 允许自动布局调整
        },
        defaultlineWidth: 4,
        defaultLineShape: 2,
        defaultNodeShape: 0,
        defaultLineFontSize: 30,
        defaultNodeBorderWidth: 0,
        defaultLineColor: 'rgb(255,255,255)',
        defaultNodeColor: 'rgba(0, 206, 209, 1)',
        lineLengths: 100,
        defaultNodeFontSize: '16px', // 全局默认字体大小

      },


      items: [
        {
          label: '通信载荷',
          expanded: false,
          children: [
            { label: '短波', selected: false, value: '短波' },
            { label: '超短波', selected: false, value: '超短波' },
          ]
        },
        {
          label: '探测载荷',
          expanded: false,
          children: [
            { label: '机载雷达', selected: false, value: '机载雷达' },
            { label: '吊放声呐', selected: false, value: '吊放声呐' },
            { label: '声呐浮标', selected: false, value: '声呐浮标' },
            { label: '光电探头', selected: false, value: '光电探头' }
          ]
        },
        {
          label: '攻击载荷',
          expanded: false,
          children: [
            { label: '航空鱼雷', selected: false, value: '航空鱼雷' },
            { label: '航空导弹', selected: false, value: '航空导弹' }
          ]
        }
      ],


      centerDialogVisible: false,
      fileListSql: [],
      //历史记录
      tableData: [],
      dialogVisibleInput: false,

      addTwType: "",
      addSpType: "",
      addDhType: "",
      addJsType: "",
      addJsInfo: "",
      editJsInfo: "",
      editJsType: "",
      twTypeList: ["全部", "起降", "飞行", "通信载荷使用", "探测载荷使用", "攻击载荷使用"],
      otherTypeList: ["全部", "起降", "飞行", "通信载荷使用", "探测载荷使用", "攻击载荷使用"],
      //动画相关
      dhParam: {
        fjlx: "",
        rwlx: "",
        zhlx: "",
        fs: 0,
        njd: 0,
        sd: 0
      },


      clickEdit: 0,

      typePic1: 0,
      typePic2: 0,
      typePic3: 0,

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
      page: "知识图谱",
      selectName: "",
      twType: "",
      pageSize: 6,
      pageNum: 1,
      total: 0,
      totalPage: 0,
      pagesList: [],
      onePagesList: [],

      infos: [],
      demoData: {},
      graphData: {
        nodes: [],
        links: []
      },
      config,
      visGraph: null, // 组件中保存VisGraph实例
      isModalVisible: false,
      isModalVisible1: false,
      newBranchContent: '',
      selectedNode: null,

      newBranchValue: '',
      newBranchFileId: '',
      newBranchLevel: null,
      newBranchParentId: '',
      newBranchRelation: '',
      typeValue: '',
      keywords: '',


      options1: [{
        value: 'D',
        label: 'D'
      }, {
        value: 'E',
        label: 'E'
      }, {
        value: 'F',
        label: 'F'
      }, {
        value: 'G',
        label: 'G'
      }],
      value1: '',


      options2: [{
        value: '对潜攻击',
        label: '对潜攻击'
      }, {
        value: '对潜搜索',
        label: '对潜搜索'
      }, {
        value: '对海攻击',
        label: '对海攻击（反舰）'
      }, {
        value: '预警侦察',
        label: '预警侦察'
      }],
      value2: '',


      options3: [],
      value3: '',


      //上传视频
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
      form: {},
      nodeInfo: {},


      //修改
      isModalVisible2: false,
      fileList: [],
      isUpload: 0,
      editName: "",
      editType: 0,
      editLeve: 0,
      editParentId: 0,
      editFileId: 0,
      editContent: 0,
      editRelation: "",
      editDhParam: {},


      //辅助决策
      shengOpen: false,
      baoContent: "",
      editBaoGao: false,
      contentData: {
        title: '标题标题标题标题标题标题标题标题标题标题',
        workGroup: '工作组111',
        content: '哈哈哈',
        date: '2016-05-02 12:02:01'
      },


      //下拉框
      showOptions1: false,
      selectedOption1: null,

      showOptions2: false,
      selectedOption2: null,

      showOptions3: false,
      selectedOption3: null,

      //修改中的类型
      editTwType: "",
      editSpType: "",
      editDhType: "",

      baoGaoName: "",
      fileTxtList: [],
      fileDocList: [],
      chooseList: [],

      uniqueArray: [],
      file: null,
      //节点
      nodes: [
        {
          "name": "j52",
          "leve": "leve2",
          "parentId": "null"
        },
        {
          "name": "j54",
          "leve": "leve2",
          "parentId": "null"
        },
        {
          "name": "j55",
          "leve": "leve2",
          "parentId": "null"
        },
        {
          "name": "z-d",
          "leve": "leve3",
          "parentId": "14238"
        },
        {
          "name": "z-f",
          "leve": "leve3",
          "parentId": "14238"
        },
        {
          "name": "z-2",
          "leve": "leve3",
          "parentId": "14240"
        },
        {
          "name": "k",
          "leve": "leve3",
          "parentId": "14238"
        },
        {
          "name": "对潜攻击",
          "leve": "leve1",
          "parentId": "14289"
        },
        {
          "name": "对潜搜索",
          "leve": "leve1",
          "parentId": "14289"
        },
        {
          "name": "对海攻击",
          "leve": "leve1",
          "parentId": "14289"
        },
        {
          "name": "预警侦察",
          "leve": "leve1",
          "parentId": "14289"
        },
        {
          "name": "起降",
          "leve": "leve4",
          "parentId": "14241"
        },
        {
          "name": "飞行",
          "leve": "leve4",
          "parentId": "14241"
        },
        {
          "name": "通信",
          "leve": "leve4",
          "parentId": "14241"
        },
        {
          "name": "探测",
          "leve": "leve4",
          "parentId": "14241"
        },
        {
          "name": "攻击",
          "leve": "leve4",
          "parentId": "14241"
        },
        {
          "name": "短波",
          "leve": "leve5",
          "parentId": "14251"
        },
        {
          "name": "超短波",
          "leve": "leve5",
          "parentId": "14251"
        },
        {
          "name": "机载雷达",
          "leve": "leve5",
          "parentId": "14252"
        },
        {
          "name": "吊放声呐",
          "leve": "leve5",
          "parentId": "14252"
        },
        {
          "name": "声呐浮标",
          "leve": "leve5",
          "parentId": "14252"
        },
        {
          "name": "光电探头",
          "leve": "leve5",
          "parentId": "14252"
        },
        {
          "name": "磁探仪",
          "leve": "leve5",
          "parentId": "14252"
        },
        {
          "name": "航空导弹",
          "leve": "leve5",
          "parentId": "14253"
        },
        {
          "name": "航空鱼雷",
          "leve": "leve5",
          "parentId": "14253"
        },
        {
          "name": "相对风",
          "leve": "leve7",
          "parentId": "14249"
        },
        {
          "name": "云底高",
          "leve": "leve7",
          "parentId": "14249"
        },
        {
          "name": "能见度",
          "leve": "leve7",
          "parentId": "14249"
        },
        {
          "name": "海况",
          "leve": "leve7",
          "parentId": "14249"
        },
        {
          "name": "风",
          "leve": "leve7",
          "parentId": "14250"
        },
        {
          "name": "降水",
          "leve": "leve7",
          "parentId": "14250"
        },
        {
          "name": "云雾",
          "leve": "leve7",
          "parentId": "14250"
        },
        {
          "name": "积冰",
          "leve": "leve7",
          "parentId": "14250"
        },
        {
          "name": "雷暴",
          "leve": "leve7",
          "parentId": "14250"
        },
        {
          "name": "电离层",
          "leve": "leve7",
          "parentId": "14254"
        },
        {
          "name": "大气波导",
          "leve": "leve7",
          "parentId": "14255"
        },
        {
          "name": "声速剖面",
          "leve": "leve7",
          "parentId": "14257"
        },
        {
          "name": "海流",
          "leve": "leve7",
          "parentId": "14257"
        },
        {
          "name": "海底地形",
          "leve": "leve7",
          "parentId": "14257"
        },
        {
          "name": "海底底质",
          "leve": "leve7",
          "parentId": "14257"
        },
        {
          "name": "降雨",
          "leve": "leve7",
          "parentId": "14256"
        },
        {
          "name": "降雪",
          "leve": "leve7",
          "parentId": "14256"
        },
        {
          "name": "冰雹",
          "leve": "leve7",
          "parentId": "14256"
        },
        {
          "name": "海杂波",
          "leve": "leve7",
          "parentId": "14256"
        },
        {
          "name": "电磁干扰",
          "leve": "leve7",
          "parentId": "14256"
        },
        {
          "name": "岛礁遮挡",
          "leve": "leve7",
          "parentId": "14260"
        },
        {
          "name": "海深",
          "leve": "leve7",
          "parentId": "14260"
        },
        {
          "name": "海底混响",
          "leve": "leve7",
          "parentId": "14260"
        },
        {
          "name": "海面混响",
          "leve": "leve7",
          "parentId": "14260"
        },
        {
          "name": "task",
          "leve": "leve0",
          "parentId": null
        }
      ],
      //关系
      relationships: [
        {
          "sourceName": "z-f",
          "targetName": "对潜攻击",
          "relationshipType": "执行"
        },
        {
          "sourceName": "z-2",
          "targetName": "对潜攻击",
          "relationshipType": "执行"
        },
        {
          "sourceName": "k",
          "targetName": "对潜攻击",
          "relationshipType": "执行"
        },
        {
          "sourceName": "z-f",
          "targetName": "对潜搜索",
          "relationshipType": "执行"
        },
        {
          "sourceName": "z-2",
          "targetName": "对潜搜索",
          "relationshipType": "执行"
        },
        {
          "sourceName": "k",
          "targetName": "对潜搜索",
          "relationshipType": "执行"
        },
        {
          "sourceName": "z-d",
          "targetName": "对海攻击",
          "relationshipType": "执行"
        },
        {
          "sourceName": "z-2",
          "targetName": "对海攻击",
          "relationshipType": "执行"
        },
        {
          "sourceName": "z-d",
          "targetName": "预警侦察",
          "relationshipType": "执行"
        },
        {
          "sourceName": "z-f",
          "targetName": "预警侦察",
          "relationshipType": "执行"
        },
        {
          "sourceName": "z-2",
          "targetName": "预警侦察",
          "relationshipType": "执行"
        },
        {
          "sourceName": "k",
          "targetName": "预警侦察",
          "relationshipType": "执行"
        },
        {
          "sourceName": "j52",
          "targetName": "z-d",
          "relationshipType": "约束"
        },
        {
          "sourceName": "j52",
          "targetName": "z-f",
          "relationshipType": "约束"
        },
        {
          "sourceName": "j52",
          "targetName": "k",
          "relationshipType": "约束"
        },
        {
          "sourceName": "j54",
          "targetName": "z-d",
          "relationshipType": "约束"
        },
        {
          "sourceName": "j54",
          "targetName": "z-f",
          "relationshipType": "约束"
        },
        {
          "sourceName": "j54",
          "targetName": "k",
          "relationshipType": "约束"
        },
        {
          "sourceName": "j55",
          "targetName": "z-d",
          "relationshipType": "约束"
        },
        {
          "sourceName": "j55",
          "targetName": "z-f",
          "relationshipType": "约束"
        },
        {
          "sourceName": "j55",
          "targetName": "z-2",
          "relationshipType": "约束"
        },
        {
          "sourceName": "z-d",
          "targetName": "起降",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-d",
          "targetName": "飞行",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-d",
          "targetName": "通信",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-d",
          "targetName": "探测",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-d",
          "targetName": "攻击",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-f",
          "targetName": "起降",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-f",
          "targetName": "飞行",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-f",
          "targetName": "通信",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-f",
          "targetName": "探测",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-f",
          "targetName": "攻击",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-2",
          "targetName": "起降",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-2",
          "targetName": "飞行",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-2",
          "targetName": "通信",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-2",
          "targetName": "探测",
          "relationshipType": "具备"
        },
        {
          "sourceName": "z-2",
          "targetName": "攻击",
          "relationshipType": "具备"
        },
        {
          "sourceName": "k",
          "targetName": "起降",
          "relationshipType": "具备"
        },
        {
          "sourceName": "k",
          "targetName": "飞行",
          "relationshipType": "具备"
        },
        {
          "sourceName": "k",
          "targetName": "通信",
          "relationshipType": "具备"
        },
        {
          "sourceName": "k",
          "targetName": "探测",
          "relationshipType": "具备"
        },
        {
          "sourceName": "k",
          "targetName": "攻击",
          "relationshipType": "具备"
        },
        {
          "sourceName": "通信",
          "targetName": "短波",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "通信",
          "targetName": "超短波",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "探测",
          "targetName": "机载雷达",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "探测",
          "targetName": "吊放声呐",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "探测",
          "targetName": "声呐浮标",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "探测",
          "targetName": "光电探头",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "探测",
          "targetName": "磁探仪",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "攻击",
          "targetName": "航空导弹",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "攻击",
          "targetName": "航空鱼雷",
          "relationshipType": "搭载"
        },
        {
          "sourceName": "相对风",
          "targetName": "起降",
          "relationshipType": "影响"
        },
        {
          "sourceName": "云底高",
          "targetName": "起降",
          "relationshipType": "影响"
        },
        {
          "sourceName": "能见度",
          "targetName": "起降",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海况",
          "targetName": "起降",
          "relationshipType": "影响"
        },
        {
          "sourceName": "风",
          "targetName": "飞行",
          "relationshipType": "影响"
        },
        {
          "sourceName": "降水",
          "targetName": "飞行",
          "relationshipType": "影响"
        },
        {
          "sourceName": "云雾",
          "targetName": "飞行",
          "relationshipType": "影响"
        },
        {
          "sourceName": "积冰",
          "targetName": "飞行",
          "relationshipType": "影响"
        },
        {
          "sourceName": "雷暴",
          "targetName": "飞行",
          "relationshipType": "影响"
        },
        {
          "sourceName": "电离层",
          "targetName": "短波",
          "relationshipType": "影响"
        },
        {
          "sourceName": "大气波导",
          "targetName": "超短波",
          "relationshipType": "影响"
        },
        {
          "sourceName": "声速剖面",
          "targetName": "吊放声呐",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海况",
          "targetName": "吊放声呐",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海流",
          "targetName": "吊放声呐",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海底地形",
          "targetName": "吊放声呐",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海底底质",
          "targetName": "吊放声呐",
          "relationshipType": "影响"
        },
        {
          "sourceName": "声速剖面",
          "targetName": "声呐浮标",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海况",
          "targetName": "声呐浮标",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海流",
          "targetName": "声呐浮标",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海底地形",
          "targetName": "声呐浮标",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海底底质",
          "targetName": "声呐浮标",
          "relationshipType": "影响"
        },
        {
          "sourceName": "降水",
          "targetName": "机载雷达",
          "relationshipType": "影响"
        },
        {
          "sourceName": "降雨",
          "targetName": "机载雷达",
          "relationshipType": "影响"
        },
        {
          "sourceName": "降雪",
          "targetName": "机载雷达",
          "relationshipType": "影响"
        },
        {
          "sourceName": "冰雹",
          "targetName": "机载雷达",
          "relationshipType": "影响"
        },
        {
          "sourceName": "云雾",
          "targetName": "机载雷达",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海杂波",
          "targetName": "机载雷达",
          "relationshipType": "影响"
        },
        {
          "sourceName": "大气波导",
          "targetName": "机载雷达",
          "relationshipType": "影响"
        },
        {
          "sourceName": "电磁干扰",
          "targetName": "机载雷达",
          "relationshipType": "影响"
        },
        {
          "sourceName": "岛礁遮挡",
          "targetName": "航空导弹",
          "relationshipType": "影响"
        },
        {
          "sourceName": "大气波导",
          "targetName": "航空导弹",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海况",
          "targetName": "航空导弹",
          "relationshipType": "影响"
        },
        {
          "sourceName": "降雨",
          "targetName": "航空导弹",
          "relationshipType": "影响"
        },
        {
          "sourceName": "云雾",
          "targetName": "航空导弹",
          "relationshipType": "影响"
        },
        {
          "sourceName": "电磁干扰",
          "targetName": "航空导弹",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海况",
          "targetName": "航空鱼雷",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海深",
          "targetName": "航空鱼雷",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海底底质",
          "targetName": "航空鱼雷",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海底混响",
          "targetName": "航空鱼雷",
          "relationshipType": "影响"
        },
        {
          "sourceName": "海面混响",
          "targetName": "航空鱼雷",
          "relationshipType": "影响"
        },
        {
          "sourceName": "task",
          "targetName": "对潜攻击",
          "relationshipType": "任务"
        },
        {
          "sourceName": "task",
          "targetName": "对潜搜索",
          "relationshipType": "任务"
        },
        {
          "sourceName": "task",
          "targetName": "对海攻击",
          "relationshipType": "任务"
        },
        {
          "sourceName": "task",
          "targetName": "预警侦察",
          "relationshipType": "任务"
        }
      ],
      clickTimer: undefined,
      rootId: undefined,
      useMove: 0,


      clickPending: false,
      clickCount: 0,
      // 长按检测
      longPressTimer: null,
      longPressThreshold: 300,
      isDragging: false,

    }
  },
  beforeDestroy() {
    clearTimeout(this.longPressTimer);
    clearTimeout(this.clickTimer);
  },
  mounted() {
    this.userType = localStorage.getItem("type");
    this.userName = localStorage.getItem("name");

    this.getFile();
    this.showGraph()
  },
  created() {


  },
  methods: {
    hhhhh(){
      console.log(this.editContent)
    },
    handleDrag(node) {
      // 初始化状态

      this.isDragging = false;

      // 开始长按检测
      this.longPressTimer = setTimeout(() => {
        if (!this.isDragging) {
          this.isDragging = true;
          this.cancelClicks();
        }
      }, this.longPressThreshold);

      // 准备单击/双击检测
      this.clickPending = true;
      this.clickCount++;

      if (this.clickCount === 1) {
        this.clickTimer = setTimeout(() => {
          if (this.clickCount === 1 && !this.isDragging) {
            this.goTextInfo(node);
          }
          this.resetClickState();
        }, 250); // 双击检测时间窗口
      } else if (this.clickCount === 2) {
        clearTimeout(this.clickTimer);
        if (!this.isDragging) {
          this.showPopup(node);
        }
        this.resetClickState();
      }
    },
    endDrag() {
      // 检查是否达到拖拽阈值
      clearTimeout(this.longPressTimer);

      if (this.isDragging) {
        // 拖拽结束处理
        this.message = "拖拽结束";
        setTimeout(() => {
          this.boxStyle = {};
          this.message = "拖拽、单击或双击我";
        }, 300);
        this.isDragging = false;
      }
    },
    handleMove(){
      this.cancelClicks()
    },
    goTextInfo(node) {
      if (!this.isDragging) {
        setTimeout(() => {
          if (this.isModalVisible == false) {
            var data = {
              'id': node.data.docId,
            }
            getInfo(data).then((res) => {


              var type = res.data.data.type;
              if (type == 1) {
                this.$router.push({
                  path: '/TwInfoXq',
                  query: {id: res.data.data.id, level: res.data.data.level, type: "tw"}
                })
              }
              if (type == 2) {
                this.$router.push({path: '/SpInfoXq', query: {id: res.data.data.id, type: "sp"}})
              }
              if (type == 3) {
                this.$router.push({path: '/DhInfoXq', query: {id: res.data.data.id, type: "dh"}})
              }
              if (type == 4) {
                this.$router.push({path: '/JsInfoXq', query: {id: res.data.data.id, type: "js"}})
              }

            });
          }
        },300)
      }
    },

    async showPopup(node) {
      if (!this.isDragging) {
        setTimeout(() => {
          this.isModalVisible = true; // 显示模态框
          this.nodeInfo = node.data;
        },300)
      }


    },

    cancelClicks() {
      this.clickPending = false;
      this.clickCount = 0;
      clearTimeout(this.clickTimer);
    },

    resetClickState() {
      this.clickCount = 0;
      this.clickPending = false;
    },
    onNodeCollapse(node) {
      // 折叠节点时，只隐藏其下层节点
      const graphInstance = this.$refs.graphRef.getInstance();
      const allNodes = graphInstance.getNodes();

      // 1. 找到所有子节点
      const childNodes = allNodes.filter(n => {
        return this.demoData.lines.some(line =>
          line.from === node.id && line.to === n.id
        );
      });

      // 2. 只隐藏子节点（不隐藏父节点）
      childNodes.forEach(child => {
        child.expanded = false;
        child.hide = true; // 可能需要根据RelationGraph的具体API调整
      });

      graphInstance.doLayout();
    },
    openFileInputData11() {
      // this.editBaoGao = false;
      this.$refs.fileInputData11.click();
    },
    handleFileUpload(event) {
      this.file = event.target.files[0];
    },
    async uploadFileZip() {
      if (!this.file) {
        alert("请选择一个文件！");
        return;
      }
      const formData = new FormData();
      formData.append("file", this.file);

      try {
        const response = await fetch("http://localhost:10035/fileUpdate/uploadZip", {
          method: "POST",
          body: formData,
        });
        const result = await response.json();
        console.log(result)
        this.$message.success("上传成功");
      } catch (error) {
        console.error("上传失败", error);
        this.$message.success("上传成功");
      }
    },


    onEditorChange1(val) {
      this.baoContent = val

    },
    sumbitChoose() {
      this.showOptions3 = false;
      const info1 = [];
      const info2 = [];
      for (let a = 0; a < this.chooseList.length; a++) {
        const currentInfo = this.chooseList[a];
        if (currentInfo != "航空鱼雷" && currentInfo != "航空导弹") {
          info1.push(currentInfo);
        } else {
          info2.push(currentInfo);
        }
      }
      var dataInfo = {
        "type": this.selectedOption2.value,
        "plane": this.selectedOption1.text,
        "info": {
          "info1": info1,
          "info2": info2,
        }
      }
      if (dataInfo.plane == "E") {
        dataInfo.plane = "z-f";
      } else if (dataInfo.plane == "F") {
        dataInfo.plane = "z-2";
      } else if (dataInfo.plane == "D") {
        dataInfo.plane = "z-d";
      } else {
        dataInfo.plane = "k"
      }
      console.log(dataInfo);
      getDomainGraphNew(dataInfo).then((res) => {
        this.zhengl(res.data);
        console.log(this.demoData)
        this.$refs.graphRef.setJsonData(this.demoData);
      })


    },
    toggleExpand(index) {
      this.items[index].expanded = !this.items[index].expanded;
    },
    handleSelect(item) {
      // 这里可以添加选择后的逻辑
      // console.log('选中:', item.label, '状态:', item.selected);
      if (item.selected == true) {
        var have = 0;
        for (let g = 0; g < this.chooseList.length; g++) {
          if (this.chooseList[g] == item.label) {
            have = 1
            break;
          }
        }
        if (have == 0) {
          this.chooseList.push(item.label)
        }
      } else {
        var kkk = this.chooseList;
        this.chooseList = [];
        for (let g = 0; g < kkk.length; g++) {
          if (kkk[g] != item.label) {
            this.chooseList.push(kkk[g])
          }
        }

      }


      // console.log(this.chooseList)
    },
    handleRemoveSql(file, fileList) {
      console.log(file, fileList);
    },
    handlePreviewSql(file) {
      console.log(file);
    },
    handleExceedSql(files, fileList) {
      this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
    },
    beforeRemoveSql(file) {
      return this.$confirm(`确定移除 ${file.name}？`);
    },


    getFile() {
      getFileId().then((res) => {
        console.log("kkkkkkkkkkkkk")
        console.log(res);
        if(res.data!="没有"){
          this.fileTxtList.push(res.data)
          this.fileDocList = res.list;
        }

      })
    },

    //导出
    exportAllContent() {
      console.log("0000000----------")
      // const loading = this.$loading({
      //   lock: true,
      //   text: '正在导出文件...',
      //   spinner: 'el-icon-loading',
      //   background: 'rgba(0, 0, 0, 0.5)',
      //   customClass: 'centered-loading'
      // });

      // 准备导出数据
      var ff = [];
      var fileNameList = [];

      for (let c = 0; c < this.fileTxtList.length; c++) {
        let fileId = this.fileTxtList[c].id;
        let allData = this.getAllItemsWithChildren(this.fileDocList, fileId);

        if (allData.length === 0) {
          continue;
        }

        ff.push(allData);
        fileNameList.push(this.fileTxtList[c].fileName);
      }

      var aa = 0;
      for (let n = 0; n < ff.length; n++) {
        // 显示加载指示器
        // this.loading = true;

        // 发送请求到后端
        // this.$axios.post('http://127.0.0.1:10035/export/exportAll', ff[n], {
        //   headers: {Authorization: "Bearer " + getToken()},
        // })

        exportAll(ff[n]).then((res) => {
          const link = document.createElement('a');
          link.href = res.data.url;
          document.body.appendChild(link);
          link.setAttribute('download', fileNameList[n]);
          link.click();
          document.body.removeChild(link);
          window.URL.revokeObjectURL(res.data.url);
          // 创建临时URL和<a>标签触发下载
          // const url = window.URL.createObjectURL(new Blob([response.data]));
          // const link = document.createElement('a');
          // link.href = url;
          // link.setAttribute('download', fileNameList[n]); // 文件名
          // document.body.appendChild(link);
          // link.click();
          aa = aa + 1;
          if (aa == ff.length) {
            this.$message.success('文件导出成功');
            // loading.close();
          }
          getFileIdData().then((res) => {
            console.log(res);
          })
          // 清除加载指示器
          // this.loading = false;
        })
          .catch(error => {
            // 错误处理
            console.error('导出失败:', error.response ? error.response.data : error.message);
            this.$message.error('导出失败，请稍后再试或联系管理员');
            // loading.close();
            // 清除加载指示器
            this.loading = false;
          });
      }
    },
    getAllItemsWithChildren(items, fileId, collected = []) {
      items.forEach(item => {
        // 如果知识点属于当前文件或它的父节点已经被收集，则收集它
        if (item.fileId === fileId || collected.some(collectedItem => collectedItem.id === item.docParentId)) {
          // 避免重复收集
          if (!collected.some(collectedItem => collectedItem.id === item.id)) {
            collected.push({
              id: item.id,
              docTitle: item.name,
              docLevel: item.level,
              fileId: item.fileId,
              docParentId: item.docParentId,
            });

            // 递归处理子项
            if (item.level2 && item.level2.length > 0) {
              this.getAllItemsWithChildren(item.level2, fileId, collected);
            }
          }
        }
      });
      return collected;
    },


    //下载方法
    downLoadInfo(row) {
      var id = row.id
      downLoadBaoGao(id).then((res) => {
        const link = document.createElement('a');
        link.href = res.data.url;
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        window.URL.revokeObjectURL(res.data.url);

      })
    },


    getAllBaoGaoHistory() {
      var data = {
        uid: localStorage.getItem("uid")
      }
      getAllHistory(data).then((res) => {
        console.log(res.list);
        this.tableData = res.list;
      })
    },
    openHistory() {
      this.clickEdit = 3;
      this.getAllBaoGaoHistory();
    },

    toggleOptions1() {
      if (this.typePic1 == 0) {
        this.typePic1 = 1;
      } else {
        this.typePic1 = 0
      }
      this.showOptions1 = !this.showOptions1;
      this.showOptions2 = false;
      this.showOptions3 = false;
    },
    selectOption1(option) {
      this.selectedOption1 = option;
      // 触发事件，通知父组件当前选中的值
      this.selectedOption1.text = option.label;
      // console.log(this.showOptions1)
      if (this.selectedOption2.text == "对潜攻击") {
        this.items = [
          {
            label: '通信载荷',
            expanded: false,
            children: [
              { label: '短波', selected: false, value: '短波' },
              { label: '超短波', selected: false, value: '超短波' },
            ]
          },
          {
            label: '探测载荷',
            expanded: false,
            children: [
              { label: '机载雷达', selected: false, value: '机载雷达' },
            ]
          },
          {
            label: '攻击载荷',
            expanded: false,
            children: [
              { label: '航空鱼雷', selected: false, value: '航空鱼雷' },
            ]
          }
        ]
      }
      if (this.selectedOption2.text == "对潜搜索") {
        if (this.selectedOption1.text == "F" || this.selectedOption1.text == "G") {
          this.items = [
            {
              label: '通信载荷',
              expanded: false,
              children: [
                { label: '短波', selected: false, value: '短波' },
                { label: '超短波', selected: false, value: '超短波' },
              ]
            },
            {
              label: '探测载荷',
              expanded: false,
              children: [
                { label: '机载雷达', selected: false, value: '机载雷达' },
                { label: '吊放声呐', selected: false, value: '吊放声呐' },
                { label: '声呐浮标', selected: false, value: '声呐浮标' },
              ]
            },
            {
              label: '攻击载荷',
              expanded: false,
              children: []
            }
          ]
        }
        if (this.selectedOption1.text == "E") {
          this.items = [
            {
              label: '通信载荷',
              expanded: false,
              children: [
                { label: '短波', selected: false, value: '短波' },
                { label: '超短波', selected: false, value: '超短波' },
              ]
            },
            {
              label: '探测载荷',
              expanded: false,
              children: [
                { label: '机载雷达', selected: false, value: '机载雷达' },
                { label: '吊放声呐', selected: false, value: '吊放声呐' },
              ]
            },
            {
              label: '攻击载荷',
              expanded: false,
              children: []
            }
          ]
        }
      }
      if (this.selectedOption2.text == "对海攻击（反舰）") {
        this.items = [
          {
            label: '通信载荷',
            expanded: false,
            children: [
              { label: '短波', selected: false, value: '短波' },
              { label: '超短波', selected: false, value: '超短波' },
            ]
          },
          {
            label: '探测载荷',
            expanded: false,
            children: [
              { label: '机载雷达', selected: false, value: '机载雷达' },
              { label: '光电探头', selected: false, value: '光电探头' },
            ]
          },
          {
            label: '攻击载荷',
            expanded: false,
            children: [
              { label: '航空导弹', selected: false, value: '航空导弹' },
            ]
          }
        ]
      }
      if (this.selectedOption2.text == "预警侦察") {
        this.items = [
          {
            label: '通信载荷',
            expanded: false,
            children: [
              { label: '短波', selected: false, value: '短波' },
              { label: '超短波', selected: false, value: '超短波' },
            ]
          },
          {
            label: '探测载荷',
            expanded: false,
            children: [
              { label: '机载雷达', selected: false, value: '机载雷达' },
            ]
          },
          {
            label: '攻击载荷',
            expanded: false,
            children: []
          }
        ]
      }

    },


    toggleOptions2() {
      if (this.typePic2 == 0) {
        this.typePic2 = 1;
      } else {
        this.typePic2 = 0
      }
      this.showOptions2 = !this.showOptions2;
      this.showOptions1 = false;
      this.showOptions3 = false;
    },
    selectOption2(option) {
      this.selectedOption2 = option;
      this.selectedOption2.text = option.label;
      if (this.selectedOption2.text == "对潜攻击") {
        this.options1 = [{
          value: 'E',
          label: 'E'
        }, {
          value: 'F',
          label: 'F'
        }, {
          value: 'G',
          label: 'G'
        }]
      }
      if (this.selectedOption2.text == "对潜搜索") {
        this.options1 = [{
          value: 'E',
          label: 'E'
        }, {
          value: 'F',
          label: 'F'
        }, {
          value: 'G',
          label: 'G'
        }]
      }
      if (this.selectedOption2.text == "对海攻击（反舰）") {
        this.options1 = [{
          value: 'D',
          label: 'D'
        }, {
          value: 'F',
          label: 'F'
        }]
      }
      if (this.selectedOption2.text == "预警侦察") {
        this.options1 = [{
          value: 'E',
          label: 'E'
        }, {
          value: 'F',
          label: 'F'
        }, {
          value: 'G',
          label: 'G'
        }, {
          value: 'D',
          label: 'D'
        }]
      }

    },


    toggleOptions3() {
      if (this.typePic3 == 0) {
        this.typePic3 = 1;
      } else {
        this.typePic3 = 0
      }
      this.showOptions3 = !this.showOptions3;
      this.showOptions2 = false;
      this.showOptions1 = false;
    },
    selectOption3(option) {
      this.selectedOption3 = option;
      // 触发事件，通知父组件当前选中的值
      this.selectedOption3.text = option.label;
    },


    downLoadWord() {
      this.clickEdit = 2;
      this.dialogVisibleInput = true;


    },
    inputName() {
      var data = {
        "uid": localStorage.getItem("uid"),
        "contentInfo": this.baoContent,
        "bgName": this.baoGaoName,
      }
      insertBaoGao(data).then((res) => {
        console.log(res);
        if (res.code == 200) {
          this.dialogVisibleInput = false;
        }

      })
    },

    cancelBaoGao() {
      this.editBaoGao = false;
      this.shengOpen = true;
    },

    openEditBao() {

      this.editBaoGao = true;

    },


    //图谱 查询

    openFileInput() {
      // 触发隐藏的文件输入框点击事件
      this.$refs.fileInput.click();
    },
    openFileInputData() {
      // this.editBaoGao = false;
      this.$refs.fileInputData.click();
    },
    handleFileChange(event) {
      const file = event.target.files[0];
      if (file) {
        // this.uploadFile1()
        this.uploadFile(file);
      }
    },
    handleFileChangeData(event) {
      const file = event.target.files[0];
      if (file) {
        this.uploadData(file);
      }
    },
    uploadData(file) {
      uploadAndExecuteSql(file)
        .then(response => {
          if (response.code === 200) {
            this.$message.success('文件上传成功');
          } else {
            this.$message.error('文件上传失败');
          }
        })
        .catch(error => {
          console.error('文件上传错误:', error);
          this.$message.error('文件上传失败');
        })
        .finally(() => {
          // 清除文件选择框的内容以便下次使用
          this.$refs.fileInput.value = null;
        });
    },
    uploadFile1() {
      createNodeAndRelationship(this.nodes, this.relationships);
    },

    uploadFile(file) {
      //添加节点和关系
      createNodeAndRelationship(this.nodes, this.relationships);
      // 调用API函数进行文件上传
      addFile(file)
        .then(response => {
          if (response.code === 200) {
            this.$message.success('文件上传成功');
          } else {
            this.$message.error('文件上传失败');
          }
        })
        .catch(error => {
          console.error('文件上传错误:', error);
          this.$message.error('文件上传失败');
        })
        .finally(() => {
          // 清除文件选择框的内容以便下次使用
          this.$refs.fileInput.value = null;
        });
    },
    goInfo(info) {
      console.log(info)
      this.$router.push('/' + info)
    },

    //管理员操作
    deleteTw() {
      var id = this.nodeInfo.docId;
      twdelete(id).then((res) => {
        console.log(res);
        if (res.code == 500) {
          this.$message.error(res.msg);
        }
        if (res.code == 200) {
          this.$message.success("删除成功");
          this.isModalVisible = false;
          this.getInfo();
        }
      })
      location.reload(true);
    },
    onCreated(editor) {
      this.editor = Object.seal(editor) // 一定要用 Object.seal() ，否则会报错
    },
    showGraph() {
      let params = {};
      getgraphInfo(params).then((res) => {
        this.zhengl(res.data);
        console.log(this.demoData);
        this.$refs.graphRef.setJsonData(this.demoData, () => {
          // const graphInstance = this.$refs.graphRef.getInstance();
          // // 重置数据
          // graphInstance.getLines().forEach(line => {
          //   if (line.text) {
          //     line.textOffset = { x: 0, y: 10 };
          //   }
          // });
        });
      })
    },
    zhengl(data) {
      console.log(data)
      const nodes = []
      const lines = [] // 存放节点和关系
      var nodeList = data.nodes;
      var lineList = data.links;
      console.log(nodeList)
      if (nodeList != undefined) {
        var root = nodeList.filter(node => node.name === 'task');
        this.rootId = root.id;


        var leve0Nodes = nodeList.filter(node => node.group === '0' && node.type === 0);
        // console.log(leve0Nodes);
        var startX = -(leve0Nodes.length * 150) / 2; // 居中起始位置

        leve0Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 0,
            x: startX + index * 200, // 水平等距排列
            y: 200,                 // leve0 的固定 Y 坐标
            fixed: true,            // 固定位置
            opacity: 0,

            properties: { ...node },
            ...style
          });
        });
        var leve1Nodes = nodeList.filter(node => node.group === '1' && node.type === 0);
        var startX1 = -(leve1Nodes.length * 270) / 2; // 居中起始位置
        leve1Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startX1 + index * 270, // 水平等距排列
            y: 400,                 // leve1 的固定 Y 坐标
            fixed: true,            // 固定位置

            data: { ...node },
            ...style
          });
        });
        var leve2Nodes = nodeList.filter(node => node.group === '2' && node.type === 0);
        var startX2 = -(leve2Nodes.length * 270) / 2 - 1000; // 居中起始位置
        leve2Nodes.forEach((node, index) => {
          console.log(node)
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 2,
            x: startX2 + index * 270, // 水平等距排列
            y: 600,                 // leve2 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: { ...node },
            ...style
          });
        });
        var leve3Nodes = nodeList.filter(node => node.group === '3' && node.type === 0);
        var startX3 = -(leve3Nodes.length * 300) / 2; // 居中起始位置
        leve3Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 3,
            x: startX3 + index * 300, // 水平等距排列
            y: 900,                 // leve3 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: { ...node },
            ...style
          });
        });
        var leve4Nodes = nodeList.filter(node => node.group === '4' && node.type === 0);
        var startX4 = -(leve4Nodes.length * 350) / 2; // 居中起始位置
        leve4Nodes.forEach((node) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          if (node.name == '起降') {
            nodes.push({
              id: node.id,
              text: node.name,
              level: 4,
              x: startX4, // 水平等距排列
              y: 1250,                 // leve4 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: { ...node },
              ...style
            });
          } else if (node.name == '飞行') {
            nodes.push({
              id: node.id,
              text: node.name,
              level: 4,
              x: startX4 + 400, // 水平等距排列
              y: 1250,                 // leve4 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: { ...node },
              ...style
            });
          } else if (node.name == '通信') {
            nodes.push({
              id: node.id,
              text: node.name,
              level: 4,
              x: startX4 + 800, // 水平等距排列
              y: 1250,                 // leve4 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: { ...node },
              ...style
            });
          } else if (node.name == '探测') {
            nodes.push({
              id: node.id,
              text: node.name,
              level: 4,
              x: startX4 + 1200, // 水平等距排列
              y: 1250,                 // leve4 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: { ...node },
              ...style
            });
          } else {
            nodes.push({
              id: node.id,
              text: node.name,
              level: 4,
              x: startX4 + 1600, // 水平等距排列
              y: 1250,                 // leve4 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: { ...node },
              ...style
            });
          }

        });
        var leve5Nodes = nodeList.filter(node => node.group === '5' && node.type === 0);
        console.log(leve5Nodes)
        var startX5 = -160; // 居中起始位置
        console.log(startX5)
        leve5Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 5,
            x: startX5 + index * 250, // 水平等距排列
            y: 1550,                 // leve5 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: { ...node },
            ...style
          });
        });
        var leve6Nodes = nodeList.filter(node => (node.group === '6' && node.type === 0) || (node.group === '7' && node.type === 0));
        // console.log(leve6Nodes)
        // if (leve6Nodes) {
        //   var startX6 = -(leve6Nodes.length * 300) / 2; // 居中起始位置
        //   leve6Nodes.forEach((node, index) => {
        //     const group = parseInt(node.group, 10);
        //     const style = this.getNodeStyle(group);
        //     nodes.push({
        //       id: node.id,
        //       text: node.name,
        //       level: 6,
        //       x: startX6 + index * 300, // 水平等距排列
        //       y: 1900,                 // leve6 的固定 Y 坐标
        //       fixed: true,            // 固定位置
        //       data: { ...node },
        //       ...style
        //     });
        //   });
        //   var startX7 = -(leve7Nodes.length * 200) / 2; // 居中起始位置
        //   leve7Nodes.forEach((node, index) => {
        //     const group = parseInt(node.group, 10);
        //     const style = this.getNodeStyle(group);
        //     nodes.push({
        //       id: node.id,
        //       text: node.name,
        //       level: 7,
        //       x: startX7 + index * 200, // 水平等距排列
        //       y: 1900,                 // leve7 的固定 Y 坐标
        //       fixed: true,            // 固定位置
        //       data: { ...node },
        //       ...style,
        //       expanded: false,
        //       expandHolderPosition: 'bottom',
        //     });
        //   });
        // } else {
        //   startX7 = -(leve7Nodes.length * 200) / 2; // 居中起始位置
        //   leve7Nodes.forEach((node, index) => {
        //     const group = parseInt(node.group, 10);
        //     const style = this.getNodeStyle(group);
        //     nodes.push({
        //       id: node.id,
        //       text: node.name,
        //       level: 7,
        //       x: startX7 + index * 200, // 水平等距排列
        //       y: 1800,                 // leve7 的固定 Y 坐标
        //       fixed: true,            // 固定位置
        //       data: { ...node },
        //       ...style,
        //       expanded: false,
        //       expandHolderPosition: 'bottom',
        //     });
        //   });
        // }
        var startX6 = -(leve6Nodes.length * 300) / 2; // 居中起始位置
          leve6Nodes.forEach((node, index) => {
            const group = parseInt(node.group, 10);
            const style = this.getNodeStyle(group);
            nodes.push({
              id: node.id,
              text: node.name,
              level: 6,
              x: startX6 + index * 300, // 水平等距排列
              y: 1900,                 // leve6 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: { ...node },
              ...style
            });
          });

        console.log(nodes);
        var NodesText1 = nodeList.filter(node => node.group === '1' && node.type != 0);
        // console.log(NodesText1)
        var startText1 = - (NodesText1.length * 200) / 2; // 居中起始位置
        NodesText1.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText1 + index * 400, // 水平等距排列
            y: 2500,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: { ...node },
            expandHolderPosition: 'bottom',
            width: 180,
            height: 180,
          });
        });
        // var NodesText2 = nodeList.filter(node => node.group === '2' && node.type != 0);
        // console.log(NodesText2)
        // var startText2 = -(NodesText2.length * 200) / 2; // 居中起始位置
        // NodesText2.forEach((node, index) => {
        //   nodes.push({
        //     id: node.id,
        //     text: node.name,
        //     level: 1,
        //     x: startText2 + index * 400, // 水平等距排列
        //     y: 2500,                 // leve7 的固定 Y 坐标
        //     fixed: true,            // 固定位置
        //     data: { ...node },
        //     width: 180,
        //     height: 180,
        //     expandHolderPosition: 'bottom',
        //   });
        // });
        var NodesText3 = nodeList.filter(node => node.group === '3' && node.type != 0);
        // console.log(NodesText3)
        var startText3 = -(NodesText3.length * 200) / 2; // 居中起始位置
        NodesText3.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText3 + index * 400, // 水平等距排列
            y: 2700,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: { ...node },
            width: 180,
            height: 180,

            expandHolderPosition: 'bottom',
          });
        });
        var NodesText4 = nodeList.filter(node => node.group === '4' && node.type != 0);
        console.log(NodesText4)
        var startText4 = -(NodesText4.length * 200) / 2; // 居中起始位置
        NodesText4.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText4 + index * 200, // 水平等距排列
            y: 2900,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: { ...node },
            width: 180,
            height: 180,

            expandHolderPosition: 'bottom',
          });
        });
        var NodesText5 = nodeList.filter(node => node.group === '5' && node.type != 0);
        // console.log(NodesText5)
        var startText5 = -(NodesText5.length * 200) / 2; // 居中起始位置
        NodesText5.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText5 + index * 200, // 水平等距排列
            y: 3100,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: { ...node },
            width: 180,
            height: 180,

            expandHolderPosition: 'bottom',
          });
        });


      }


      if (lineList != undefined) {
        var leve0Lines = lineList.filter(line => line.relate === '任务');
        // console.log(leve0Lines);
        leve0Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 4,
            lineShape: 1,
            isHide: true,
          });
        });
        var leve1Lines = lineList.filter(line => line.relate === '执行');
        // console.log(leve1Lines);
        leve1Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 4,
            // lineShape: 3,
            // textOffset_x: 0, // 文字X轴偏移量
            // textOffset_y: 200, // 文字Y轴偏移量
            color: '#fff',
            lineShape: 1,
            useTextPath: true
          });
        });
        var leve2Lines = lineList.filter(line => line.relate === '约束');
        // console.log(leve2Lines);
        leve2Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 4,
            // lineShape: 3,
            color: '#000',
            lineShape: 1,
            useTextPath: true
          });
        });
        var leve3Lines = lineList.filter(line => line.relate === '具备');
        // console.log(leve3Lines);
        leve3Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 4,
            color: '#FFFF00',
            lineShape: 1,
            useTextPath: true
          });
        });
        var leve4Lines = lineList.filter(line => line.relate === '搭载');
        // console.log(leve4Lines);
        leve4Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 4,
            color: 'rgb(84,251,128)',
            lineShape: 1,
            useTextPath: true
          });
        });
        var leve5Lines = lineList.filter(line => line.relate === '包含');
        // console.log(leve5Lines);
        leve5Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 4,
            color: '#fff',
            lineShape: 1,
            useTextPath: true
          });
        });
        var leve6Lines = lineList.filter(line => line.relate === '影响');
        // console.log(leve6Lines);
        leve6Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 4,
            color: '#ffbf71',
            lineShape: 1,
            useTextPath: true
          });
        });
        var leve7Lines = lineList.filter(line => line.relate !== '任务' && line.relate !== '执行' && line.relate !== '约束' && line.relate !== '具备' && line.relate !== '搭载' && line.relate !== '包含' && line.relate !== '影响');
        console.log("属于：")
        console.log(leve7Lines)
        leve7Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 4,

            color: '#FF0000',
            lineShape: 1,
            useTextPath: true
          });
        });
        // for (let b = 0; b < lineList.length; b++) {
        //   const sourceId = lineList[b].source;
        //   const targetId = lineList[b].target;

        //   // 检查 source 和 target 是否存在于节点的 id 中
        //   const sourceNodeExists = nodes.some(node => node.id === sourceId);
        //   const targetNodeExists = nodes.some(node => node.id === targetId);
        //   if (!sourceNodeExists) {
        //     console.error(`Source node with id ${sourceId} not found.`);
        //     continue; // 跳过该连线
        //   }
        //   if (!targetNodeExists) {
        //     console.error(`Target node with id ${targetId} not found.`);
        //     continue; // 跳过该连线
        //   }
        //   lines.push({
        //     from: lineList[b].source,
        //     to: lineList[b].target,
        //     text: lineList[b].relate,
        //     lineWidth: 4,
        //     lineShape: 3,
        //   })
        // }
      }
      this.demoData = {
        "rootId": this.rootId,
        "nodes": nodes,
        "lines": lines
      }
    },
    // eslint-disable-next-line no-unused-vars
    // async showPopup(node) {
    //   clearTimeout(this.clickTimer);
    //
    //   this.isModalVisible = true; // 显示模态框
    //   this.nodeInfo = node.data;
    // },
    async openAdd() {
      this.selectedNode = this.nodeInfo;
      this.newBranchParentId = this.nodeInfo.docId;
      this.newBranchLevel = parseInt(this.nodeInfo.group) + 1;
      try {
        const response = await this.getFileIdByDocId({ docId: this.nodeInfo.docId });

        this.newBranchFileId = response.fileId;
        console.log(this.newBranchFileId)
        this.isModalVisible1 = true;
      } catch (error) {
        console.error('Failed to fetch file ID:', error);
        alert('无法获取文件ID，请稍后再试。');
        return;
      }
    },
    async openEdit() {
      this.isModalVisible2 = true;
      var data = {
        'id': this.nodeInfo.docId,
      }
      console.log(this.nodeInfo.docId)
      getInfo(data).then((res) => {
        console.log(res.data)
        if (res.data.data.type == 1) {
          this.editType = "tw";
        }
        if (res.data.data.type == 2) {
          this.editType = "sp";
        }
        if (res.data.data.type == 3) {
          this.editType = "dh";
        }
        if (res.data.data.type == 4) {
          this.editType = "js";
        }

        this.editName = res.data.data.name;
        this.editLeve = res.data.data.level;
        this.editParentId = res.data.data.parentId;
        this.editFileId = res.data.data.fileId;
        // this.editRelation = res.data.data.relation;
        console.log(res.data.data)
        if (this.editType == 'tw') {
          this.editTwType = res.data.data.twType;
          this.editContent = res.data.data.contentInfo;
          var imgs = res.data.data.imgList;
          console.log(imgs)
          this.fileList = [];

          for (let j = 0; j < imgs.length; j++) {
            var ii = {
              uuid: imgs[j].imgId,
              url: imgs[j].imgUrl
            }
            this.fileList.push(ii)
          }
        }
        if (this.editType == 'sp') {
          this.editSpType = res.data.data.spType;
          this.videoFileList = [];
          this.showVideoPath = "";
          if (res.data.data.spUrl != null) {
            this.videoFileList.push({ url: res.data.data.spUrl, name: res.data.data.name });
            this.showVideoPath = res.data.data.spUrl;
          }
        }
        if (this.editType == 'dh') {
          this.editDhType = res.data.data.dwType;

          this.videoFileList = [];
          this.showVideoPath = "";
          if (res.data.data.dwUrl != null) {
            this.videoFileList.push({ url: res.data.data.dwUrl, name: res.data.data.name });
            this.showVideoPath = res.data.data.dwUrl;
          }

          // var dhParam = JSON.parse(res.data.data.dwUrl)
          //   this.editDhParam = {
          //     fjlx:dhParam.fjlx,
          //     rwlx:dhParam.rwlx,
          //     zhlx:dhParam.zhlx,
          //     fs:dhParam.fs,
          //     njd:dhParam.njd,
          //     sd:dhParam.sd
          //   };
        }
        if (this.editType == 'js') {
          this.editJsInfo = res.data.data.jsInfo;
          this.editJsType = res.data.data.jsType;

        }

      });
    },
    async editSubmit() {
      if (this.editType == 'tw') {
        const content = this.editName
        const value = this.editContent
        const fileId = this.editFileId
        const relation = this.editRelation

        if (content) {
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
          // 构造数据
          const data = {
            id: this.nodeInfo.docId,
            fileId: fileId,
            name: content,
            contentInfo: value,
            relation: relation,
            parentId: this.editParentId,
            level: this.editLeve,
            type: 1,
            imgs: urlStr,
            twType: this.editTwType
          };

          try {
            editInfoGraph(data).then((res) => {
              console.log(res);
              this.isModalVisible2 = false;
              this.editContent = ""
            })

            // 刷新图谱

            // this.closeModal(); // 关闭模态框

          } catch (error) {
            console.error('Failed to add new branch:', error);
            alert('Failed to add new branch. Please try again.');
          }
        }
      }


      if (this.editType == 'sp') {
        const content = this.editName.trim();
        const relation = this.editRelation.trim();
        console.log(this.videoFileList[0].url);

        if (content) {
          // 构造数据
          const data = {
            id: this.nodeInfo.docId,
            type: 2,
            name: content,
            relation: relation,
            parentId: this.editParentId,
            level: this.editLeve,
            spUrl: this.videoFileList[0].url,
            spType: this.editSpType
          };

          try {
            editInfoGraph(data).then((res) => {
              console.log(res);
              this.isModalVisible2 = false;
            })

            // 刷新图谱

          } catch (error) {
            console.error('Failed to add new branch:', error);
            alert('Failed to add new branch. Please try again.');
          }
        }
      }


      if (this.editType == 'dh') {
        const content = this.editName.trim();
        const relation = this.editRelation.trim();
        var dwurl = this.videoFileList[0].url;
        const data = {
          id: this.nodeInfo.docId,
          type: 3,
          name: content,
          relation: relation,
          parentId: this.editParentId,
          level: this.editLeve,
          dwUrl: dwurl,
          dwType: this.editDhType
        };
        try {
          editInfoGraph(data).then((res) => {
            console.log(res);
            this.isModalVisible2 = false;
          })

          // 刷新图谱

        } catch (error) {
          console.error('Failed to add new branch:', error);
          alert('Failed to add new branch. Please try again.');
        }
      }


      if (this.editType == 'js') {
        const content = this.editName.trim();
        console.log(this.editRelation.trim() + content)
        const relation = this.editRelation.trim();
        console.log("123")
        const data = {
          id: this.nodeInfo.docId,
          type: 4,
          name: content,
          relation: relation,
          parentId: this.editParentId,
          level: this.editLeve,
          jsInfo: this.editJsInfo,
          jsType: this.editJsType
        };
        try {
          editInfoGraph(data).then((res) => {
            console.log(res);
            this.isModalVisible2 = false;
          })

          // 刷新图谱

        } catch (error) {
          console.error('Failed to add new branch:', error);
          alert('Failed to add new branch. Please try again.');
        }
      }

      location.reload(true);
    },


    //上传照片请
    //照片墙
    // 处理图片移除
    handleRemove(file, fileList) {
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

    getFileIdByDocId(data) {
      return getFileIdByDocId(data);
    },
    closeModal() {
      this.isModalVisible1 = false;
      this.newBranchContent = '';
      this.selectedNode = null;
    },

    closeModal1() {
      this.isModalVisible2 = false;
      this.editContent = '';
      this.selectedNode = null;
    },
    async addNewBranch() {
      this.isModalVisible = false;
      if (this.typeValue == 'tw') {
        const content = this.newBranchContent.trim();
        const value = this.newBranchValue.trim();
        const fileId = this.newBranchFileId.trim();
        const relation = this.newBranchRelation.trim();

        if (this.selectedNode && content && value) {

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


          // 构造数据
          const data = {
            fileId: fileId,
            txtName: content,
            TxtValue: value,
            relation: relation,
            parentId: this.newBranchParentId,
            level: this.newBranchLevel,
            nodeType: 'tw',
            imgs: urlStr,
            twType: this.addTwType
          };

          try {
            await addNode(data);

            // 创建新节点

            this.closeModal(); // 关闭模态框
            this.isModalVisible = false;
          } catch (error) {
            console.error('Failed to add new branch:', error);
            alert('Failed to add new branch. Please try again.');
          }
        }
      }


      if (this.typeValue == 'sp') {
        console.log(this.videoFileList[0].url)
        const content = this.newBranchContent.trim();
        const relation = this.newBranchRelation.trim();

        if (this.selectedNode && content) {
          // 构造数据
          const data = {
            nodeType: this.typeValue,
            txtName: content,
            relation: relation,
            parentId: this.newBranchParentId,
            level: this.newBranchLevel,
            spUrl: this.videoFileList[0].url,
            spType: this.addSpType
          };

          try {
            await addNode(data);


            this.closeModal(); // 关闭模态框
          } catch (error) {
            console.error('Failed to add new branch:', error);
            alert('Failed to add new branch. Please try again.');
          }
        }
      }

      //动画
      if (this.typeValue == 'dh') {
        const content = this.newBranchContent.trim();
        const relation = this.newBranchRelation.trim();
        var dhParamInfo = this.videoFileList[0].url;
        // var dhParamInfo =  JSON.stringify(this.dhParam);

        if (this.selectedNode && content) {
          // 构造数据
          const data = {
            nodeType: this.typeValue,
            txtName: content,
            relation: relation,
            parentId: this.newBranchParentId,
            level: this.newBranchLevel,
            DhParams: dhParamInfo,
            dwType: this.addDhType
          };

          try {
            await addNode(data);
            this.closeModal(); // 关闭模态框
          } catch (error) {
            console.error('Failed to add new branch:', error);
            alert('Failed to add new branch. Please try again.');
          }
        }
      }

      if (this.typeValue == 'js') {
        const content = this.newBranchContent.trim();
        const relation = this.newBranchRelation.trim();


        if (this.selectedNode && content) {
          if(this.fileId==null){
            const data = {
              nodeType: this.typeValue,
              parentType: "0",
              txtName: content,
              relation: relation,
              parentId: this.newBranchParentId,
              level: this.newBranchLevel,
              jsType: this.addJsType,
              jsInfo: this.addJsInfo
            };
            console.log(data);
            try {
              await addNode(data);


              this.closeModal(); // 关闭模态框
            } catch (error) {
              console.error('Failed to add new branch:', error);
              alert('Failed to add new branch. Please try again.');
            }
          }else {
            const data = {
              nodeType: this.typeValue,

              txtName: content,
              relation: relation,
              parentId: this.newBranchParentId,
              level: this.newBranchLevel,
              jsType: this.addJsType,
              jsInfo: this.addJsInfo
            };
            try {
              await addNode(data);


              this.closeModal(); // 关闭模态框
            } catch (error) {
              console.error('Failed to add new branch:', error);
              alert('Failed to add new branch. Please try again.');
            }
          }
          // 构造数据



        }
      }

      if (this.typeValue == '') {
        const content = this.newBranchContent.trim();
        const relation = this.newBranchRelation.trim();

        if (this.selectedNode && content) {
          // 构造数据
          const data = {
            nodeType: '0',
            txtName: content,
            relation: relation,
            parentId: this.newBranchParentId,
            level: this.newBranchLevel,
          };

          try {
            console.log(data);
            await addNode(data);


            this.closeModal(); // 关闭模态框
          } catch (error) {
            console.error('Failed to add new branch:', error);
            alert('Failed to add new branch. Please try again.');
          }
        }
      }
      location.reload(true);
    },
    // 执行布局算法

    getNodeStyle(group) {
      const styles = [
        { width: 150, height: 150, color: "#ef7a43", fontColor: '255,255,255', size: '60px' },
        { width: 250, height: 250, color: '#ffa384', font: 'normal 40px Arial', fontColor: '0,0,0' },
        { width: 230, height: 230, color: '#00f6ff', font: 'normal 50px Arial', fontColor: '0,0,0' },
        { width: 210, height: 210, color: '#00c6ff', font: 'normal 40px Arial', fontColor: '0,0,0' },
        { width: 200, height: 200, color: '#2a98ff', font: 'normal 32px Arial', fontColor: '#ffffff' },
        { width: 200, height: 200, color: '#005fb7', font: 'normal 30px Arial', fontColor: '#ffffff' },
        { width: 200, height: 200, color: '#003ea4', font: 'normal 28px Arial', fontColor: '#ffffff' },
        { width: 190, height: 190, color: '#7df887', font: 'normal 28px Arial', fontColor: '#000000' }
      ];

      return styles[group] || {};
    },
    getNodeStyle1(group) {
      const styles = [
        { size: 450, width: 450, height: 450, color: '255,111,62' },
        { size: 350, width: 350, height: 350, color: '255,163,132' },
        { size: 300, width: 300, height: 300, color: '0,246,255' },
        { size: 250, width: 250, height: 250, color: '0,198,255' },
        { size: 200, width: 200, height: 200, color: '42,152,255' },
        { size: 150, width: 150, height: 150, color: '0,95,183' },
        { size: 130, width: 130, height: 130, color: '0,62,164' }
      ];

      return styles[group] || {};
    },

    //视频相关
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

  },


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


.rightList {
  width: 96%;
  height: 88%;
  position: absolute;
  z-index: 2;
  margin-top: 1%;
  margin-left: 2.6%;
  margin-bottom: 5%;
  border-radius: 1vw 1vw 1vw 1vw;
}

.rightListContent {
  width: 100%;
  height: 100%;
  position: absolute;
  z-index: 2;
  top: 1%;

}

.tupu {
  width: 100%;
  height: 95%;
  position: absolute;
  z-index: 3;
  top: 7.5%;
}

.gContainer {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  width: 100%;
  height: 38vw;
  border-radius: 2vw;
  background-color: rgba(163, 196, 245, 0.78);
  margin-top: 0.5vw;
}

/*background-color: rgba(152, 193, 255, 0.62);*/
.oneRight {
  width: 98%;
  height: 5vw;
  line-height: 5vw;
  margin: 0 1%;
  display: flex;
  flex-direction: row;
  text-align: center;
  color: #ffffff;
}

.pageList {
  height: 1.5vw;
  width: 20%;
  margin: 0 40%;
  position: absolute;
  z-index: 2;
  bottom: -0.5%;
  display: flex;
  flex-direction: row;
  color: #ffffff;
}

.custom-dialog {
  margin-top: 0vh !important;
}


.graphcontains1 {
  width: 60%;
  height: 2vw;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-left: 5%;

}

.graphcontains2 {
  width: 40%;
  height: 2vw;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-left: 1%;

}

input {
  width: 100%;
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
  color: rgba(255, 255, 255, 0.54);
  opacity: 1;
  /* Firefox 默认将 placeholder 的透明度设置为 0.54 */

}


select {
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
  color: white;
  /* 文字颜色 */
  background-color: transparent;
  padding-left: 3%;
  position: absolute;
  z-index: 2000;
  appearance: none;
}

option {
  color: black;
  background: rgb(255, 255, 255);
  line-height: 20px;
}

option:hover {
  background: #EBCCD1;
}

.bgBao {
  width: 50vw;
  height: 35vw;
  border-radius: 1vw;
  background-color: transparent;
  position: absolute;
  z-index: 5001;
  left: 26%;
  top: 19%;
}

.baoGaoContentInfo {
  ::v-deep img {
    width: 100% !important;
  }
}


/*滚动条高宽度*/
.baoGaoContentInfo::-webkit-scrollbar {
  width: 8px;
  height: 4px;
}

/*滚动条滑块*/
.baoGaoContentInfo::-webkit-scrollbar-thumb {
  border-radius: 3px;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  background: #76ceff;
}

/*滚动条里面轨道*/
.baoGaoContentInfo ::-webkit-scrollbar-track {
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.2) inset;

}

/*滚动条的小边角*/
.baoGaoContentInfo::-webkit-scrollbar-corner {
  background: transparent;
}

.el-dialog .custom-dialog1 {
  height: 47vw !important;
}

.custom-select {
  position: relative;
  width: 12vw;
  cursor: pointer;
  height: 85%;
  line-height: 1.5vw;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}

.selected-option {
  text-align: center;
  line-height: 1.7vw;
  width: 7vw;
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
}

.option {
  margin-bottom: 0.2vw !important;
  margin-left: 0.5vw;

}

.option:hover {
  background-image: url("../assets/img/optionSelect.png");
  background-size: 100% 100%;
  color: #000000;

}


.cascade-select {
  font-family: Arial, sans-serif;
  user-select: none;
  max-width: 300px;
}

.cascade-select ul {
  list-style: none !important;
  padding-left: 20px;
  margin: 5px 0;
}

.cascade-select li {
  margin: 8px 0;
  list-style: none !important;
}

.parent-item {
  font-weight: normal;
  cursor: pointer;
  display: flex;
  align-items: center;
  padding: 0.2vw 0.5vw;
  font-size: 0.8vw;
}

.parent-item:hover {
  background-image: url("../assets/img/optionSelect.png");
  background-size: 100% 100%;
  color: #000000;
}

.arrow {
  font-size: 10px;
  margin-right: 8px;
  transition: transform 0.2s;
  display: inline-block;
}

.arrow.expanded {
  transform: rotate(90deg);
}

label {
  cursor: pointer;
  display: flex;
  align-items: center;
}

input[type="checkbox"] {
  margin-right: 8px;
}

.selected-items {
  margin-top: 20px;
  padding: 10px;
  border-top: 1px solid #eee;
}

.selected-items h4 {
  margin-bottom: 8px;
}

ul {
  list-style: none;
  padding: 0 !important;
}

.level-1 {
  background-image: url("../assets/img/optionBg.png");
  background-size: 100% 100%;
  position: absolute;
  top: 93%;
  left: 38%;
  right: 0;
  list-style-type: none;
  padding: 0;
  margin: 0;
  z-index: 5000;
  background-color: transparent;
  max-height: 150px;
  overflow-y: auto;
}

/*滚动条高宽度*/
.level-1::-webkit-scrollbar {
  width: 8px;
  height: 4px;
}

/*滚动条滑块*/
.level-1::-webkit-scrollbar-thumb {
  border-radius: 3px;
  box-shadow: inset 0 0 5px rgba(129, 129, 129, 0.16);
  background: #22ceff;
}

/*滚动条里面轨道*/
.level-1 ::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px rgba(129, 129, 129, 0.16);
}

/* 富文本编辑器获取的html是纯html,需要全局设置样式,.middle-raw只对这个组件起作用不影响其他样式 */
:deep(.baoGaoInfotest) {
  font-size: 14px;
  height: calc(100vh - 160px);
  width: 900px;
  position: relative;
  z-index: 999;

  .scrollable {
    max-height: calc(100vh - 160px);
    /* 设置最大高度 */
    overflow-y: auto;
    /* 纵向出现滚动条 */
    overflow-x: hidden;
    /* 隐藏横向滚动条（如果需要） */
    padding: 10px;
    /* 内边距 */
  }

  table {
    border: 1px solid #666;
    margin: 10px;
    width: 100%;
  }

  table td,
  table th {
    border-bottom: 1px solid #666;
    border-right: 1px solid #666;
    padding: 3px 5px;
    text-align: center;
    /* 中心对齐 */
    vertical-align: middle;
    /* 垂直方向居中对齐 */
  }
}


.baoGaoInfotest table {
  border: 1px solid #232222 !important;
}

.baoGaoInfotest table th,
.baoGaoInfotest table td {
  border: 1px solid #3c3a3a !important;
}

.baoGaoInfotest table td {
  padding: 0px 5px !important;
}

::v-deep .rel-map {
  background: none !important;

  .rel-node-shape-1 {
    background: rgba(255, 255, 255, 0.2) !important;
    border-radius: 10px;
    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
  }
}

::v-deep .rel-toolbar {
  color: #ffffff;
  background: rgba(34, 206, 255, 0.51);

  .c-current-zoom {
    color: #ffffff;
  }
}

::v-deep textPath{
  font-size: 30px !important;
}

.my-graph {
  background: transparent;
}

.tyg {
  font-size: 2vw !important;
}
::v-deep .c-rg-line-text {
  font-size: 8px !important; /* 最小字体大小 */
  opacity: 1 !important;
  visibility: visible !important;
  pointer-events: none;
}

</style>
