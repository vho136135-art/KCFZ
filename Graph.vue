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
                <div class="oneMulu" v-if="page!=item.name" @click="goInfo(item.info)">
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
                       style="width: 19vw;height: 6vw;position: absolute;bottom: -3vw;left: -3.5vw;z-index: -1;"/>
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
              <input
                  type="text"
                  placeholder="请输入关键词"
                  v-model="keywords"
                  @keyup.enter="getInfo1()"
              />
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
                   v-if="typePic2==0">
              <img src="../assets/img/graphUp.png"
                   style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                   v-if="typePic2==1">
              <ul v-if="showOptions2" class="options">
                <li
                    v-for="(option, index) in options2"
                    :key="index"
                    @click="selectOption2(option)"
                    class="option"
                >
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
                   v-if="typePic1==0">
              <img src="../assets/img/graphUp.png"
                   style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                   v-if="typePic1==1">
              <ul v-if="showOptions1" class="options">
                <li
                    v-for="(option, index) in options1"
                    :key="index"
                    @click="selectOption1(option)"
                    class="option"
                >
                  {{ option.label }}
                </li>
              </ul>
            </div>
          </div>
        </div>

        <div class="graphcontains2">
          <div class="custom-select">
            <div style="font-size: 1vw;width: 6vw;">飞机载荷:</div>
            <div style="width: 10vw;position: relative;">
              <img src="../assets/img/graphInput.png" style="position: absolute;z-index: 99;width:100%;height: 100%;">

              <div class="selected-option">
                {{ selectedOption3 ? selectedOption3.text : '请选择载荷' }}
              </div>
              <img src="../assets/img/graphDown.png"
                   style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                   @click="toggleOptions3"
                   v-if="typePic3==0">
              <img src="../assets/img/graphUp.png" @click="toggleOptions3"
                   style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                   v-if="typePic3==1">
              <ul class="level-1" v-if="showOptions3">
                <li v-for="(item, index) in items" :key="'level1-'+index">
                  <!-- 第一层 - 不可选，仅作为分类 -->
                  <div class="parent-item" @click="toggleExpand(index)">
                    <span class="arrow" :class="{ expanded: item.expanded }">▶</span>
                    {{ item.label }}
                  </div>

                  <!-- 第二层 - 可选 -->
                  <ul class="level-2" v-show="item.expanded" style="margin-left: 1vw;">
                    <li v-for="(subItem, subIndex) in item.children" :key="'level2-'+subIndex">
                      <label style="font-size: 0.8vw;">
                        <input
                            style="position: relative;width: 1vw;"
                            type="checkbox"
                            v-model="subItem.selected"
                            @change="handleSelect(subItem)"
                        >
                        {{ subItem.label }}
                      </label>
                    </li>
                  </ul>
                </li>
              </ul>
            </div>

          </div>
        </div>
        <div
            style="width: 10vw;background-color: #00f6ff;height: 1.7vw;line-height: 1.7vw;border-radius: 1vw;text-align: center;margin-left: 1vw;"
            @click="sumbitChoose()">查询
        </div>


      </div>
      <div
          style="width: 24%;display: flex;flex-direction: row;position: absolute;height: 1.7vw;right: 2vw;z-index: 2000;justify-content: space-around;margin-top: 1%;">
        <div style="width:21%;" v-if="userType==1">
          <div
              style="height: 1.7vw;width: 100%;background-color: transparent;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0vw 0.1vw;border: 1px #2ed0d6 solid;justify-items: center;align-items: center;"
              @click="openFileInputData">
            <img src="../assets/img/Inicon.png" style="height: 60%;object-fit: contain;">
            <div style="color: #FFFFFF;margin-left: 0.25vw;font-size: 0.9vw;">导入资源</div>
          </div>
          <input
              ref="fileInputData"
              type="file"
              accept=".doc, .docx"
              style="display: none;"
              @change="handleFileChangeData"
          />

        </div>
        <div style="width:21%;" v-if="userType==1" >
          <div
              style="height: 1.7vw;width: 100%;background-color: transparent;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0vw 0.1vw;border: 1px #2ed0d6 solid;justify-items: center;align-items: center;"
              @click="openEditBao">
            <img src="../assets/img/Inicon.png" style="height: 60%;object-fit: contain;">
            <div style="color: #FFFFFF;margin-left: 0.25vw;font-size: 0.9vw;">资源文件</div>
          </div>

        </div>
        <div style="width:20%;" v-if="userType==1" @click="exportAllContent">
          <div
              style="height: 1.7vw;width: 100%;background-color: transparent;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0vw 0.1vw;border: 1px #2ed0d6 solid;justify-items: center;align-items: center;"
              >
            <div style="color: #FFFFFF;margin-left: 0.25vw;font-size: 0.9vw;">导出</div>
          </div>
        </div>
        <div style="width:20%;" v-if="userType==1">
          <div
              style="height: 1.7vw;width: 100%;background-color: transparent;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0vw 0.1vw;border: 1px #2ed0d6 solid;justify-items: center;align-items: center;"
              @click="openFileInput">
            <img src="../assets/img/Inicon.png" style="height: 60%;object-fit: contain;">
            <div style="color: #FFFFFF;margin-left: 0.25vw;font-size: 0.9vw;">导入</div>
          </div>
          <input
              ref="fileInput"
              type="file"
              accept=".doc, .docx"
              style="display: none;"
              @change="handleFileChange"
          />


        </div>
        <!--        <div style="margin-left: 0.5vw;width: 35%;margin-top: 0.6vw;">-->
        <!--          <div-->
        <!--              style="height: 1.7vw;width: 5.5vw;background-color: #2ed0d6;border-radius: 1vw;display: flex;flex-direction: row;justify-content: center;padding: 0 0.1vw;border: 1px #2ed0d6 solid;"-->
        <!--              @click="shengcheng()">-->
        <!--            <img src="../assets/img/shengchengicon.png" style="height: 1vw;object-fit: contain;margin-top: 0.2vw;">-->
        <!--            <div style="line-height: 1.7vw;color: #FFFFFF;margin-left: 0.25vw;">辅助决策</div>-->
        <!--          </div>-->
        <!--          <input-->
        <!--              ref="fileInput"-->
        <!--              type="file"-->
        <!--              accept=".doc, .docx"-->
        <!--              style="display: none;"-->
        <!--              @change="handleFileChange"-->
        <!--          />-->
        <!--        </div>-->

      </div>

      <div class="rightContent">
        <div class="rightList">
          <div class="tupu">
            <div style="width: 100%;height: 100%;">
              <div class="gContainer">
                <div id="graph-panel" style="width: 100%;height: 100%;"></div>
              </div>
            </div>
          </div>
          <!-- 操作弹窗 -->
          <el-dialog
              title="操作分支内容"
              :visible.sync="isModalVisible"
              append-to-body
              top="10vh"
              custom-class="custom-dialog"
          >

            <el-form label-width="90px">
              <el-form-item label="节点名称">
                <el-input v-model="nodeInfo.name" readonly></el-input>
              </el-form-item>
              <el-form-item label="节点层级">
                <el-input v-model="nodeInfo.leve" readonly></el-input>
              </el-form-item>
              <el-form-item label="操作">
                <el-button type="primary" @click="openAdd()">新增下级</el-button>
                <el-button type="warning" @click="openEdit()">修改</el-button>
                <el-button type="danger" @click="deleteTw()">删除</el-button>
              </el-form-item>
            </el-form>
          </el-dialog>


          <!--     新增分支弹窗     -->
          <el-dialog
              title="添加分支内容"
              :visible.sync="isModalVisible1"
              append-to-body
              top="4vh"
              custom-class="custom-dialog"
          >
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

              <el-form-item style="position: relative ;" label="图文类别" v-if="this.typeValue=='tw'">
                <el-select v-model="addTwType" placeholder="请选择类别">
                  <el-option
                      v-for="item in twTypeList"
                      :key="item"
                      :label="item"
                      :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item style="position: relative ;" label="视频类别" v-if="this.typeValue=='sp'">
                <el-select v-model="addSpType" placeholder="请选择类别">
                  <el-option
                      v-for="item in otherTypeList"
                      :key="item"
                      :label="item"
                      :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item style="position: relative ;" label="动画类别" v-if="this.typeValue=='dh'">
                <el-select v-model="addDhType" placeholder="请选择类别">
                  <el-option
                      v-for="item in otherTypeList"
                      :key="item"
                      :label="item"
                      :value="item">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item style="position: relative ;" label="计算类别" v-if="this.typeValue=='js'">
                <el-select v-model="addJsType" placeholder="请选择类别">
                  <el-option
                      v-for="item in otherTypeList"
                      :key="item"
                      :label="item"
                      :value="item">
                  </el-option>
                </el-select>
              </el-form-item>


              <el-form-item label="节点名称">
                <el-input v-model="newBranchContent"></el-input>
              </el-form-item>
              <el-form-item label="计算模块地址" v-if="this.typeValue=='js'">
                <el-input v-model="addJsInfo"></el-input>
              </el-form-item>

              <el-form-item style="position: relative ;" label="节点内容" v-if="this.typeValue=='tw'">
                <Editor v-model="newBranchValue" style="height: 10vw;margin-bottom: 5vw;"></Editor>
              </el-form-item>

              <el-form-item style="position: relative;" label="相关图片" v-if="this.typeValue=='tw'">
                <el-upload
                    action="http://127.0.0.1:10035/fileUpdate/upload"
                    list-type="picture-card"
                    :on-remove="handleRemove"
                    :file-list="fileList"
                    :multiple="true"
                    :limit="9"
                    :on-exceed="handleExceed"
                    :before-upload="beforeUpload"
                    :on-success="handleSuccess"
                    :on-error="handleError">
                  <i class="el-icon-plus"></i>
                </el-upload>
              </el-form-item>


              <el-form-item label="上传视频" prop="spUrl" v-if="this.typeValue=='sp' || this.typeValue=='dh'">
                <el-upload
                    class="avatar-uploader el-upload--text"
                    multiple
                    :headers="videoUpload.headers"
                    :action="videoUpload.url"
                    :file-list="videoFileList"
                    :show-file-list="false"
                    accept=".mp4"
                    :on-success="handleVideoSuccess"
                    :before-upload="beforeUploadVideo"
                    :on-progress="uploadVideoProcess"
                    :on-remove="handleVideoRemove"
                >
                  <div v-if="!videoFlag && showVideoPath" style="display: flex; flex-wrap: wrap; gap: 10px;">
                    <!--                    <div v-for="(url, index) in showVideoPath.split(',')" :key="url"-->
                    <!--                         style="position: relative; flex: 1 1 calc(33.333% - 20px); min-width: 200px; margin-bottom: 10px;">-->
                    <video :src="showVideoPath" style="width:50%; height: auto;border-radius: 0.5vw;"
                           class="avatar video-avatar" controls>
                      您的浏览器不支持视频播放
                    </video>
                    <img
                        src="../assets/img/delete.png"
                        @click.stop="handleVideoRemove(videoFileList[0])"
                        style="width: 35px; height: 35px;position: absolute; top: 5px; left: 5px; cursor: pointer; z-index: 999;"
                        alt="删除"
                    />
                    <!--                    </div>-->
                  </div>
                  <el-progress :stroke-width="10" class="progressType" v-if="videoFlag"
                               type="circle" :percentage="videoUploadPercent" style="margin-top:30px;"></el-progress>
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
          <el-dialog
              title="修改分支内容"
              :visible.sync="isModalVisible2"
              append-to-body
              top="1vh"
              style="height: 55vw;"
              custom-class="custom-dialog"
          >
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
              <el-form-item style="position: relative ;" label="图文类别" v-if="this.editType=='tw'">
                <el-select v-model="editTwType" placeholder="请选择图文类别">
                  <el-option
                      v-for="item in twTypeList"
                      :key="item"
                      :label="item"
                      :value="item">
                  </el-option>
                </el-select>
              </el-form-item>


              <el-form-item style="position: relative ;" label="视频类别" v-if="this.editType=='sp'">
                <el-select v-model="editSpType" placeholder="请选择视频类别">
                  <el-option
                      v-for="item in otherTypeList"
                      :key="item"
                      :label="item"
                      :value="item">
                  </el-option>
                </el-select>
              </el-form-item>


              <el-form-item style="position: relative ;" label="动画类别" v-if="this.editType=='dh'">
                <el-select v-model="editDhType" placeholder="请选择类别">
                  <el-option
                      v-for="item in otherTypeList"
                      :key="item"
                      :label="item"
                      :value="item">
                  </el-option>
                </el-select>
              </el-form-item>

              <el-form-item style="position: relative ;" label="计算模块类别" v-if="this.editType=='js'">
                <el-select v-model="editJsType" placeholder="请选择类别">
                  <el-option
                      v-for="item in otherTypeList"
                      :key="item"
                      :label="item"
                      :value="item">
                  </el-option>
                </el-select>
              </el-form-item>


              <el-form-item label="计算模块地址" v-if="this.editType=='js'">
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

              <el-form-item style="position: relative ;margin-bottom: 5vw;" label="节点内容" v-if="this.editType=='tw'">
                <Editor v-model="this.editContent" style="height: 6vw;"></Editor>
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
              <el-form-item style="position: relative;" label="相关图片" v-if="this.editType=='tw'">
                <el-upload
                    action="http://127.0.0.1:10035/fileUpdate/upload"
                    list-type="picture-card"
                    :on-remove="handleRemove"
                    :file-list="fileList"
                    :multiple="true"
                    :limit="9"
                    :on-exceed="handleExceed"
                    :before-upload="beforeUpload"
                    :on-success="handleSuccess"
                    :on-error="handleError">
                  <i class="el-icon-plus"></i>
                </el-upload>
              </el-form-item>

              <el-form-item label="上传视频" prop="spUrl" v-if="this.editType=='sp' || this.editType=='dh'">
                <el-upload
                    class="avatar-uploader el-upload--text"
                    multiple
                    :headers="videoUpload.headers"
                    :action="videoUpload.url"
                    :file-list="videoFileList"
                    :show-file-list="false"
                    accept=".mp4"
                    :on-success="handleVideoSuccess"
                    :before-upload="beforeUploadVideo"
                    :on-progress="uploadVideoProcess"
                    :on-remove="handleVideoRemove"
                >

                  <div v-if="!videoFlag && showVideoPath" style="display: flex; flex-wrap: wrap; gap: 10px;">
                    <div
                        style="position: relative; flex: 1 1 calc(33.333% - 20px); min-width: 200px; margin-bottom: 10px;">

                      <video :src="showVideoPath" style="width:50%; height: auto;border-radius: 0.5vw;"
                             class="avatar video-avatar" controls>
                        您的浏览器不支持视频播放
                      </video>
                      <img
                          src="../assets/img/delete.png"
                          @click.stop="handleVideoRemove(videoFileList[0])"
                          style="width: 35px; height: 35px;position: absolute; top: 5px; left: 5px; cursor: pointer; z-index: 999;"
                          alt="删除"
                      />
                    </div>
                  </div>
                  <el-progress :stroke-width="10" class="progressType" v-if="videoFlag"
                               type="circle" :percentage="videoUploadPercent" style="margin-top:30px;"></el-progress>
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
           @click="shengOpen=false">
      <div class="bgBao">
        <img src="../assets/img/baoGaobg.png" style="height: 100%;object-fit: contain;position: absolute;z-index: -5;">

        <div
            style="width: 2vw;height: 7vw;background-color: transparent;position: absolute;top: 10%;left: 1.8%;display: flex;flex-direction: column;justify-content: center;">
          <img src="../assets/img/baoGaoEdit.png"
               style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit==0"
               @click="openEditBao()">
          <img src="../assets/img/baoGaoDown.png"
               style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;"
               v-if="clickEdit==0" @click="downLoadWord()">
          <img src="../assets/img/history.png" style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;"
               @click="openHistory" v-if="clickEdit==0">

          <img src="../assets/img/baoGaoEdit1.png"
               style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit==1">
          <img src="../assets/img/baoGaoDown.png"
               style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;"
               v-if="clickEdit==1" @click="downLoadWord()">
          <img src="../assets/img/history.png" style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;"
               @click="openHistory" v-if="clickEdit==1">


          <img src="../assets/img/baoGaoEdit.png"
               style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit==2"
               @click="openEditBao()">
          <img src="../assets/img/baoGaoDown1.png"
               style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;"
               v-if="clickEdit==2">
          <img src="../assets/img/history.png" style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;"
               @click="openHistory" v-if="clickEdit==2">


          <img src="../assets/img/baoGaoEdit.png"
               style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;" v-if="clickEdit==3"
               @click="openEditBao()">
          <img src="../assets/img/baoGaoDown.png"
               style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;margin-bottom: 0.5vw;"
               @click="downLoadWord()" v-if="clickEdit==3">
          <img src="../assets/img/history1.png" style="width: 1.5vw;object-fit: contain;margin-left: 0.25vw;"
               v-if="clickEdit==3">
        </div>

        <div
            style="font-weight: 500;width: 35%;height: 4.5vw;background-color: transparent;
            margin-top: 0.2vw;margin-left: 5%;display: flex;flex-direction: row;justify-content: center;">

          <img src="../assets/img/baoJian.png"
               style="height: 1.2vw;object-fit: contain;margin-top: 1.65vw;margin-right: 10%;">
          <div style="line-height: 4.5vw;font-size: 1.5vw;color: #00f6ff;">
            报告
          </div>


        </div>
        <div class="baoGaoContentInfo"
             style="width: 85%;height: 76%;background-color: transparent;margin-left: 6%;margin-top: 0.5vw;padding: 0 2vw;overflow-y: scroll;">
          <div v-if="clickEdit!=3" class="baoGaoInfotest" style="line-height: 2vw;color: #ffffff;" v-html="baoContent"
               :key="this.editBaoGao"></div>


          <el-table v-else
                    :data="tableData"
                    style="width: 90%;margin-top: 2vw;margin-left: 5%;">
            <el-table-column
                prop="bgName"
                label="报告名称"
                header-align="center"
                align="center">
            </el-table-column>
            <el-table-column
                prop="name"
                label="操作"
                header-align="center"
                align="center">
              <template slot-scope="scope">
                <el-button
                    size="mini"
                    @click="lookInfo(scope.row)">编辑
                </el-button>
                <el-button
                    size="mini"
                    type="warning"
                    @click="downLoadInfo(scope.row)">下载
                </el-button>
                <el-button
                    size="mini"
                    type="danger"
                    @click="delteInfo(scope.row)">删除
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
    <el-dialog
        title="上传视频，动画以及计算"
        :visible.sync="centerDialogVisible"
        width="30%"
        center>
      <el-upload
          class="upload-demo"
          action="http://127.0.0.1:10035/file/uploadAndExecuteSqls"
          :on-remove="handleRemoveSql"
          :before-remove="beforeRemoveSql"
          multiple
          :limit="3"
          :on-exceed="handleExceedSql"
          :file-list="fileListSql">
        <el-button size="small" type="primary">点击上传</el-button>

      </el-upload>
      <span slot="footer" class="dialog-footer">
    <el-button @click="centerDialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
  </span>
    </el-dialog>

    <!--     新增分支弹窗     -->
    <el-dialog
        title="上传资源" :visible.sync="editBaoGao"
        append-to-body
        top="4vh"

    >
      <div style="display: flex;">
        <div style="margin-left: 1vw;width:20%;">
          <div
              style="height: 100%;width: 50%;background-color:#2ed0d6 ;border-radius: 0.3vw;display: flex;flex-direction: row;justify-content: center;border: 1px #2ed0d6 solid;"
              @click="openFileInputData11">
            <div style="line-height: 2.5vw;color: #FFFFFF;margin-left: 0.25vw;">选取文件</div>
          </div>
          <input
              ref="fileInputData11"
              type="file"
              accept=".doc, .docx"
              style="display: none;"
              @change="handleFileUpload"
          />

        </div>
        <el-button type="success" @click="uploadFileZip">上传</el-button>
      </div>



    </el-dialog>


    <el-dialog
        title="报告名称"
        :visible.sync="dialogVisibleInput"
        width="30%">
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
import {editInfoGraph, getInfo} from "@/api/kcInfo";
import {getDomainGraphNew, getgraphInfo} from "@/api/login";
import VisGraph from '@/assets/js/graphvis.min.20241008.js'
import LayoutFactory from '@/assets/js/graphvis.layout.min.js'
import {config} from '@/assets/defaultConfig.js'
import {addFile, addNode, getFileIdByDocId, uploadAndExecuteSql} from "@/api/file";
import Editor from "@/components/EditorUse.vue";
import {getToken} from "@/utils/auth";
import {twdelete} from "@/api/twdelete";
import {downLoadBaoGao, getAllHistory, getBaoGaoInfo, insertBaoGao} from "@/api/baogao";
import {exportAll, getFileId, getFileIdData} from "@/api/export";
// , exportToWord,

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Graph',
  components: {Editor, Foot, headInfo},
  computed: {
    selectedItems() {
      return this.items
          .flatMap(item => item.children)
          .filter(child => child.selected);
    }
  },
  data() {
    return {
      items: [
        {
          label: '通信载荷',
          expanded: false,
          children: [
            {label: '短波', selected: false, value: '短波'},
            {label: '超短波', selected: false, value: '超短波'},
          ]
        },
        {
          label: '探测载荷',
          expanded: false,
          children: [
            {label: '机载雷达', selected: false, value: '机载雷达'},
            {label: '吊放声呐', selected: false, value: '吊放声呐'},
            {label: '声呐浮标', selected: false, value: '声呐浮标'},
            {label: '光电探头', selected: false, value: '光电探头'}
          ]
        },
        {
          label: '攻击载荷',
          expanded: false,
          children: [
            {label: '航空鱼雷', selected: false, value: '航空鱼雷'},
            {label: '航空导弹', selected: false, value: '航空导弹'}
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
      twTypeList: ["全部", "海洋大气", "海洋文学", "海洋地理", "复杂水声", "复杂电磁"],
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


      options1: [],
      value1: '',


      options2: [{
        value: '对潜攻击',
        label: '对潜攻击'
      }, {
        value: '对潜搜索',
        label: '对潜搜索'
      }, {
        value: '对海攻击（反舰）',
        label: '对海攻击（反舰）'
      }, {
        value: '预警侦查',
        label: '预警侦查'
      }
      ],
      value2: '',


      options3: [],
      value3: '',


      //上传视频
      //上传的视频
      videoUpload: {
        // 设置上传的请求头部
        headers: {Authorization: "Bearer " + getToken()},
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

      uniqueArray:[],
      file: null,


    }

  },
  mounted() {
    this.userType = localStorage.getItem("type");
    this.userName = localStorage.getItem("name");
    this.getInfo();
    this.getFile();
  },
  created() {


    var that = this;


    //节点的点击事件
    this.config.node.onClick = function (event, node) {

      console.log(node.properties);
      var data = {
        'id': node.properties.docId,
      }
      getInfo(data).then((res) => {

        var type = res.data.data.type;
        if (type == 1) {
          that.$router.push({path: '/TwInfoXq', query: {id: res.data.data.id, level: res.data.data.level, type: "tw"}})
        }
        if (type == 2) {
          that.$router.push({path: '/SpInfoXq', query: {id: res.data.data.id, type: "sp"}})
        }
        if (type == 3) {
          that.$router.push({path: '/DhInfoXq', query: {id: res.data.data.id, type: "dh"}})
        }
        if (type == 4) {
          that.$router.push({path: '/JsInfoXq', query: {id: res.data.data.id, type: "js"}})
        }

      });
    };
  },
  methods: {
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
      console.log(this.chooseList);
      var dataInfo = {
        "type": this.selectedOption2.text,
        "plane": this.selectedOption1.text,
        "info": this.chooseList
      }
      var graphUse = [];

      console.log(dataInfo)

      //通信
      for(let a=0;a<dataInfo.info.length;a++){
        if (dataInfo.info[a] == "短波") {
          graphUse.push("电离层")
        }
        if (dataInfo.info[a] == "超短波") {
          graphUse.push("大气波导")
        }

        //探测
        if (dataInfo.info[a] == "吊放声呐") {
          graphUse.push("声速剖面")
          graphUse.push("海况")
          graphUse.push("海流")
          graphUse.push("海底地形")
          graphUse.push("海底底质")
        }
        if (dataInfo.info[a] == "声呐浮标") {
          graphUse.push("声速剖面")
          graphUse.push("海况")
          graphUse.push("海流")
          graphUse.push("海底地形")
          graphUse.push("海底底质")
        }
        if (dataInfo.info[a] == "机载雷达") {
          graphUse.push("降水")
          graphUse.push("降雨")
          graphUse.push("降雪")
          graphUse.push("冰雹")
          graphUse.push("云雾")
          graphUse.push("海杂波")
          graphUse.push("大气波导")
          graphUse.push("电磁干扰")
        }
        if (dataInfo.info[a].indexOf("鱼雷") !== -1) {
          graphUse.push("海况")
          graphUse.push("海深")
          graphUse.push("海底地质")
          graphUse.push("海底混响")
          graphUse.push("海面混响")
        }
        if (dataInfo.info[a].indexOf("导弹") !== -1) {
          graphUse.push("倒角遮挡")
          graphUse.push("大气波导")
          graphUse.push("海况")
          graphUse.push("降雨")
          graphUse.push("云雾")
          graphUse.push("电磁干扰")
        }
      }

      this.uniqueArray = graphUse.filter((item, index) => graphUse.indexOf(item) === index);


      let params = {
        keywords: this.uniqueArray,
      };
      getDomainGraphNew(params).then((res) => {
        this.zhengl(res.data);
      })





      // chooseBaoGaoGraph(dataInfo).then((res) => {
      //   console.log(res);
      // })

    },
    toggleExpand(index) {
      this.items[index].expanded = !this.items[index].expanded;
      this.showOptions3 = true
    },
    handleSelect(item) {
      // 这里可以添加选择后的逻辑
      console.log('选中:', item.label, '状态:', item.selected);
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


      console.log(this.chooseList)
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
        console.log(res.list);
        this.fileTxtList.push(res.data)
        this.fileDocList = res.list;
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
    },
    selectOption1(option) {
      this.selectedOption1 = option;
      this.showOptions1 = false;
      // 触发事件，通知父组件当前选中的值
      this.selectedOption1.text = option.label;
      if (this.selectedOption2.text == "对潜攻击") {
        this.items = [
          {
            label: '通信载荷',
            expanded: false,
            children: [
              {label: '短波', selected: false, value: '短波'},
              {label: '超短波', selected: false, value: '超短波'},
            ]
          },
          {
            label: '探测载荷',
            expanded: false,
            children: [
              {label: '机载雷达', selected: false, value: '机载雷达'},
            ]
          },
          {
            label: '攻击载荷',
            expanded: false,
            children: [
              {label: '航空鱼雷', selected: false, value: '航空鱼雷'},
            ]
          }
        ]
      }
      if (this.selectedOption2.text == "对潜搜索") {
        if (this.selectedOption1.text == "C" || this.selectedOption1.text == "D") {
          this.items = [
            {
              label: '通信载荷',
              expanded: false,
              children: [
                {label: '短波', selected: false, value: '短波'},
                {label: '超短波', selected: false, value: '超短波'},
              ]
            },
            {
              label: '探测载荷',
              expanded: false,
              children: [
                {label: '机载雷达', selected: false, value: '机载雷达'},
                {label: '吊放声呐', selected: false, value: '吊放声呐'},
                {label: '声呐浮标', selected: false, value: '声呐浮标'},
              ]
            },
            {
              label: '攻击载荷',
              expanded: false,
              children: []
            }
          ]
        }
        if (this.selectedOption1.text == "A") {
          this.items = [
            {
              label: '通信载荷',
              expanded: false,
              children: [
                {label: '短波', selected: false, value: '短波'},
                {label: '超短波', selected: false, value: '超短波'},
              ]
            },
            {
              label: '探测载荷',
              expanded: false,
              children: [
                {label: '机载雷达', selected: false, value: '机载雷达'},
                {label: '吊放声呐', selected: false, value: '吊放声呐'},
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
      if (this.selectedOption2.text == "对海攻击(反舰)") {
        this.items = [
          {
            label: '通信载荷',
            expanded: false,
            children: [
              {label: '短波', selected: false, value: '短波'},
              {label: '超短波', selected: false, value: '超短波'},
            ]
          },
          {
            label: '探测载荷',
            expanded: false,
            children: [
              {label: '机载雷达', selected: false, value: '机载雷达'},
              {label: '光电探头', selected: false, value: '光电探头'},
            ]
          },
          {
            label: '攻击载荷',
            expanded: false,
            children: [
              {label: '航空导弹', selected: false, value: '航空导弹'},
            ]
          }
        ]
      }
      if (this.selectedOption2.text == "预警侦查") {
        this.items = [
          {
            label: '通信载荷',
            expanded: false,
            children: [
              {label: '短波', selected: false, value: '短波'},
              {label: '超短波', selected: false, value: '超短波'},
            ]
          },
          {
            label: '探测载荷',
            expanded: false,
            children: [
              {label: '机载雷达', selected: false, value: '机载雷达'},
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
    },
    selectOption2(option) {
      this.selectedOption2 = option;
      this.showOptions2 = false;
      this.selectedOption2.text = option.label;

      if (this.selectedOption2.text == "对潜攻击") {
        this.options1 = [{
          value: 'A',
          label: 'A'
        }, {
          value: 'C',
          label: 'C'
        }, {
          value: 'D',
          label: 'D'
        }]
      }
      if (this.selectedOption2.text == "对潜搜索") {
        this.options1 = [{
          value: 'A',
          label: 'A'
        }, {
          value: 'C',
          label: 'C'
        }, {
          value: 'D',
          label: 'D'
        }]
      }
      if (this.selectedOption2.text == "对海攻击(反舰)") {
        this.options1 = [{
          value: 'A',
          label: 'A'
        }, {
          value: 'C',
          label: 'C'
        }]
      }
      if (this.selectedOption2.text == "预警侦查") {
        this.options1 = [{
          value: 'A',
          label: 'A'
        }, {
          value: 'C',
          label: 'C'
        }, {
          value: 'D',
          label: 'D'
        }, {
          value: 'A',
          label: 'A'
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
    },
    selectOption3(option) {
      this.selectedOption3 = option;
      this.showOptions3 = false;
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
    submitBaoGao() {


      this.editBaoGao = false;
      this.shengOpen = true;
      this.clickEdit = 0;

      console.log("djhaskdhjkashd---------")
      console.log(this.baoContent)
      this.baoContent = this.baoContent.replaceAll('<table', '<table style="border: 1px solid #232222;"');
      this.baoContent = this.baoContent.replaceAll('<td', '<td style="border: 1px solid #232222;"');
      this.baoContent = this.baoContent.replaceAll('<th', '<th style="border: 1px solid #232222;"');
      // this.baoContent.replaceAll("table","table style="\  "\")


    },
    openEditBao() {

      this.editBaoGao = true;

    },
    shengcheng() {
      console.log("这里是辅助决策的按钮")
      this.shengOpen = true;
      console.log(this.graphData.nodes)
      //循环这些数据放进去
      var one = "";
      var two = "";
      var three = "";
      var four = "";
      var five = "";
      var six = "";
      var seven = "";
      for (let a = 0; a < this.graphData.nodes.length; a++) {
        var level = this.graphData.nodes[a].properties.leve
        if (level == '1') {
          if (one == "") {
            one = this.graphData.nodes[a].properties.docId
          } else {
            one = one + "," + this.graphData.nodes[a].properties.docId
          }
        }
        if (level == '2') {
          if (two == "") {
            two = this.graphData.nodes[a].properties.docId
          } else {
            two = two + "," + this.graphData.nodes[a].properties.docId
          }
        }
        if (level == '3') {

          if (three == "") {
            three = this.graphData.nodes[a].properties.docId
          } else {
            three = three + "," + this.graphData.nodes[a].properties.docId
          }
        }
        if (level == '4') {
          if (four == "") {
            four = this.graphData.nodes[a].properties.docId
          } else {
            four = four + "," + this.graphData.nodes[a].properties.docId
          }
        }
        if (level == '5') {
          if (five == "") {
            five = this.graphData.nodes[a].properties.docId
          } else {
            five = five + "," + this.graphData.nodes[a].properties.docId
          }
        }
        if (level == '6') {
          if (six == "") {
            six = this.graphData.nodes[a].properties.docId
          } else {
            six = six + "," + this.graphData.nodes[a].properties.docId
          }
        }
        if (level == '7') {
          if (seven == "") {
            seven = this.graphData.nodes[a].properties.docId
          } else {
            seven = seven + "," + this.graphData.nodes[a].properties.docId
          }
        }


      }


      var data = {
        "one": one,
        "two": two,
        "three": three,
        "four": four,
        "five": five,
        "six": six,
        "seven": seven
      }
      //辅助决策内容
      getBaoGaoInfo(data).then((res) => {
        this.baoContent = res;
      })

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


    uploadFile(file) {
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
    },
    onCreated(editor) {
      this.editor = Object.seal(editor) // 一定要用 Object.seal() ，否则会报错
    },
    getInfo() {
      this.graphData = undefined;
      this.demoData = {}

      if (this.keywords != '' && this.keywords != undefined) {
        this.visGraph.clearAll();
        let params = {
          nodename: this.keywords,
        };
        getgraphInfo(params).then((res) => {
          this.zhengl(res.data);
        })
      } else {

        let params = {};
        getgraphInfo(params).then((res) => {
          this.zhengl(res.data);
        })
      }
    },
    getInfo1() {
      this.graphData = undefined;
      this.demoData = {}

      if (this.keywords != '' && this.keywords != undefined) {
        this.visGraph.clearAll();
        let params = {
          nodename: this.keywords,
        };
        getgraphInfo(params).then((res) => {
          this.zhengl(res.data);
        })
      } else {
        this.visGraph.clearAll();
        let params = {};
        getgraphInfo(params).then((res) => {
          this.zhengl(res.data);
        })
      }
    },
    async drawGraphData() {
      this.graphData = this.demoData;
      if (this.visGraph === null) {
        this.createGraph();
        // this.genrateGraphData();
        // this.visGraph.showNodeRightMenu()
        this.visGraph.drawData(this.graphData);
        this.visGraph.incremaNodesCodinate(this.graphData.nodes);
        this.reLayout();
      } else {
        this.createGraph();
        this.visGraph.drawData(this.graphData);
        this.visGraph.incremaNodesCodinate(this.graphData.nodes);
        this.reLayout();
      }
      this.loading = false;
    },
    // 创建全局绘图客户端对象
    createGraph() {
      const configWithEvents = {
        ...this.config,
        node: {
          ...this.config.node,
          ondblClick: (event, node) => {
            if (this.userType == 1) {
              this.showPopup(node);
            }

            console.log("dkdlskdlakldksl")

          }
        }
      };

      console.log(configWithEvents)
      this.visGraph = new VisGraph(document.getElementById('graph-panel'), configWithEvents);
    },
    // eslint-disable-next-line no-unused-vars
    async showPopup(node) {
      console.log("dkjalsjdkljsdalkaj")
      console.log(node)
      this.isModalVisible = true; // 显示模态框
      this.nodeInfo = node.properties;
    },
    async openAdd() {
      this.selectedNode = this.nodeInfo;
      this.newBranchParentId = this.nodeInfo.docId;
      this.newBranchLevel = parseInt(this.nodeInfo.leve) + 1;
      try {
        const response = await this.getFileIdByDocId({docId: this.nodeInfo.docId});

        this.newBranchFileId = response.fileId;
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
      getInfo(data).then((res) => {
        console.log(res.data.data)
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
        this.editRelation = res.data.data.relation;
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
            this.videoFileList.push({url: res.data.data.spUrl, name: res.data.data.name});
            this.showVideoPath = res.data.data.spUrl;
          }
        }
        if (this.editType == 'dh') {
          this.editDhType = res.data.data.dwType;

          this.videoFileList = [];
          this.showVideoPath = "";
          if (res.data.data.dwUrl != null) {
            this.videoFileList.push({url: res.data.data.dwUrl, name: res.data.data.name});
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
            })

            // 刷新图谱
            this.visGraph.drawData(this.graphData);
            this.reLayout();
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
            this.visGraph.drawData(this.graphData);
            this.reLayout();
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
          this.visGraph.drawData(this.graphData);
          this.reLayout();
        } catch (error) {
          console.error('Failed to add new branch:', error);
          alert('Failed to add new branch. Please try again.');
        }
      }


      if (this.editType == 'js') {
        const content = this.editName.trim();
        const relation = this.editRelation.trim();

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
          this.visGraph.drawData(this.graphData);
          this.reLayout();
        } catch (error) {
          console.error('Failed to add new branch:', error);
          alert('Failed to add new branch. Please try again.');
        }
      }


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
            const newNodeId = Date.now().toString(); // 使用时间戳作为唯一ID
            const newNode = {
              id: newNodeId,
              label: content,
              properties: {name: content, docId: newNodeId, level: this.newBranchLevel},
              ...this.getNodeStyle(this.newBranchLevel) // 根据层级应用样式
            };
            const newLink = {
              source: this.selectedNode.id,
              target: newNodeId,
              type: '',
            };
            this.graphData.nodes.push(newNode);
            this.graphData.links.push(newLink);

            // 刷新图谱
            this.visGraph.drawData(this.graphData);
            this.reLayout();
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

            // 创建新节点
            const newNodeId = Date.now().toString(); // 使用时间戳作为唯一ID
            const newNode = {
              id: newNodeId,
              label: content,
              properties: {name: content, docId: newNodeId, level: this.newBranchLevel},
              ...this.getNodeStyle(this.newBranchLevel) // 根据层级应用样式
            };
            const newLink = {
              source: this.selectedNode.id,
              target: newNodeId,
              type: '',
            };
            this.graphData.nodes.push(newNode);
            this.graphData.links.push(newLink);

            // 刷新图谱
            this.visGraph.drawData(this.graphData);
            this.reLayout();
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

            // 创建新节点
            const newNodeId = Date.now().toString(); // 使用时间戳作为唯一ID
            const newNode = {
              id: newNodeId,
              label: content,
              properties: {name: content, docId: newNodeId, level: this.newBranchLevel},
              ...this.getNodeStyle(this.newBranchLevel) // 根据层级应用样式
            };
            const newLink = {
              source: this.selectedNode.id,
              target: newNodeId,
              type: '',
            };
            this.graphData.nodes.push(newNode);
            this.graphData.links.push(newLink);

            // 刷新图谱
            this.visGraph.drawData(this.graphData);
            this.reLayout();
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
          // 构造数据
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

            // 创建新节点
            const newNodeId = Date.now().toString(); // 使用时间戳作为唯一ID
            const newNode = {
              id: newNodeId,
              label: content,
              properties: {name: content, docId: newNodeId, level: this.newBranchLevel},
              ...this.getNodeStyle(this.newBranchLevel) // 根据层级应用样式
            };
            const newLink = {
              source: this.selectedNode.id,
              target: newNodeId,
              type: '',
            };
            this.graphData.nodes.push(newNode);
            this.graphData.links.push(newLink);

            // 刷新图谱
            this.visGraph.drawData(this.graphData);
            this.reLayout();
            this.closeModal(); // 关闭模态框
          } catch (error) {
            console.error('Failed to add new branch:', error);
            alert('Failed to add new branch. Please try again.');
          }
        }
      }

    },
    // 执行布局算法
    reLayout(alpha) {
      var that = this;
      if (alpha == null) {
        that.visLayout = null;
        that.visLayout = new LayoutFactory(this.visGraph.getGraphData()).createLayout('fastFR');
        that.visLayout.resetConfig({
          label: {
            show: true
          },
          friction: 0.8,
          linkDistance: 400,
          linkStrength: 0.2,
          charge: -1000,
          gravity: 0.01,
          noverlap: true,
          size: [that.visGraph.stage.width, that.visGraph.stage.height]
        });
      } else {
        that.visLayout.alpha += (alpha > 1 ? 0.2 : alpha); //继续运动
      }

      runLayout();//开始继续动画执行

      //通过动画帧控制控制布局算法的执行，有动画效果
      function runLayout() {
        cancelAnimationFrame(that.layoutLoopName);//停止动画控制
        that.visLayout.runLayout();  //运行布局算法
        that.visGraph.refresh();
        if (that.visLayout.alpha > 0.05) {
          that.layoutLoopName = requestAnimationFrame(runLayout);
        } else {
          if (that.visGraph.currentNode && that.visGraph.currentNode.isDragging) {
            that.visLayout.alpha = 0.1; //继续运动
            that.layoutLoopName = requestAnimationFrame(runLayout);
          } else {
            that.visLayout.alpha = 0; //停止运动
            cancelAnimationFrame(that.layoutLoopName);
          }
        }
      }

      // this.autoLayout();
    },
    zhengl(data) {
      const nodes = []
      const links = [] // 存放节点和关系

      var nodeList = data.nodes;
      var lineList = data.links;
      var allOne = ""

      console.log(nodeList)
      if (nodeList != undefined) {
        allOne = nodeList[0].docId
        for (let a = 0; a < nodeList.length; a++) {
          const group = parseInt(nodeList[a].group, 10);
          const style = this.getNodeStyle(group);


          if (nodeList[a].type == 4) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
            nodes.push({
              id: nodeList[a].id,
              label: " ",
              shape: 'circle',
              showlabel: true,
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,
              },
              image: "http://127.0.0.1:10035/profile/jsq.png",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 3) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
            nodes.push({
              id: nodeList[a].id,
              label: " ",
              shape: 'circle',
              showlabel: true,
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,
              },
              image: "http://127.0.0.1:10035/profile/dhvideoPic.png",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 2) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
            nodes.push({
              id: nodeList[a].id,
              label: " ",
              shape: 'circle',
              showlabel: true,
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,
              },
              image: "http://127.0.0.1:10035/profile/videoPic.png",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else {
            nodes.push({
              id: nodeList[a].id,
              label: nodeList[a].name,
              shape: 'circle',
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,

              },
              image: "http://127.0.0.1:10035/profile/tw.png",

              headTipText: "附加信息",
              ...style, // 展开 style 对象以应用样式属性

            });
          }


        }
      }

      // var allOne = nodeList[0].docId


      if (lineList != undefined) {
        for (let b = 0; b < lineList.length; b++) {

          var bbb = {name: lineList[b].relate}
          links.push({
            source: lineList[b].source,
            target: lineList[b].target,
            type: lineList[b].relate,
            properties: bbb,
            color: '202,202,202',
            lineWidth: 3,
          })
        }
      }


      this.demoData = {
        "nodes": nodes,
        "links": links
      }
      this.drawGraphData();
    },
    // color: '255,111,62',

    getNodeStyle(group) {
      const styles = [
        {size: 450, width: 450, height: 450, color: '255,111,62', font: 'normal 68px Arial', fontColor: '255,255,255'},
        {size: 350, width: 350, height: 350, color: '255,163,132', font: 'normal 68px Arial', fontColor: '255,255,255'},
        {size: 300, width: 300, height: 300, color: '0,246,255', font: 'normal 50px Arial', fontColor: '0,0,0'},
        {size: 250, width: 250, height: 250, color: '0,198,255', font: 'normal 40px Arial', fontColor: '0,0,0'},
        {size: 200, width: 200, height: 200, color: '42,152,255', font: 'normal 32px Arial', fontColor: '255,255,255'},
        {size: 150, width: 150, height: 150, color: '0,95,183', font: 'normal 30px Arial', fontColor: '0,0,0'},
        {size: 130, width: 130, height: 130, color: '0,62,164', font: 'normal 28px Arial', fontColor: '255,255,255'}
      ];

      return styles[group] || {};
    },
    getNodeStyle1(group) {
      const styles = [
        {size: 450, width: 450, height: 450, color: '255,111,62'},
        {size: 350, width: 350, height: 350, color: '255,163,132'},
        {size: 300, width: 300, height: 300, color: '0,246,255'},
        {size: 250, width: 250, height: 250, color: '0,198,255'},
        {size: 200, width: 200, height: 200, color: '42,152,255'},
        {size: 150, width: 150, height: 150, color: '0,95,183'},
        {size: 130, width: 130, height: 130, color: '0,62,164'}
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
        this.videoFileList.push({url: videoUrl, name: file.name});
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
  background-color: rgba(152, 193, 255, 0.62);
  margin-top: 1vw;
}

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
  color: white; /* 文字颜色 */
  background-color: transparent;
  padding-left: 3%;
  position: absolute;
  z-index: 2000;

}

input::placeholder {
  color: rgba(255, 255, 255, 0.54);
  opacity: 1; /* Firefox 默认将 placeholder 的透明度设置为 0.54 */

}


select {
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
  color: white; /* 文字颜色 */
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
  top: 110%;
  left: 0;
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
    max-height: calc(100vh - 160px); /* 设置最大高度 */
    overflow-y: auto; /* 纵向出现滚动条 */
    overflow-x: hidden; /* 隐藏横向滚动条（如果需要） */
    padding: 10px; /* 内边距 */
  }

  table {
    border: 1px solid #666;
    margin: 10px;
    width: 100%;
  }

  table td, table th {
    border-bottom: 1px solid #666;
    border-right: 1px solid #666;
    padding: 3px 5px;
    text-align: center; /* 中心对齐 */
    vertical-align: middle; /* 垂直方向居中对齐 */
  }
}


.baoGaoInfotest table {
  border: 1px solid #232222 !important;
}

.baoGaoInfotest table th, .baoGaoInfotest table td {
  border: 1px solid #3c3a3a !important;
}

.baoGaoInfotest table td {
  padding: 0px 5px !important;
}
</style>
