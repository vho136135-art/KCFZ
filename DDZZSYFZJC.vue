<template>
  <div class="background-container">
    <div class="content-container">
      <div
          style="display: flex;width: 96%;margin-left: 12vw;margin-bottom: 1.5vh;margin-top: 1.5vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color: #fff; font-size: 1.6vw;font-weight: 500;">
          舰载直升机空舰导弹作战使用辅助决策软件
        </div>
        <el-button type="primary" class="button1" style="height: 1.5vw;margin-left: 30vw;" @click="save">保存
        </el-button>
      </div>
      <div style="display: flex;width: 95%;height: 87%;" class="waibiankuang">
        <div style="display: flex;">
          <div style="display: flex;flex-direction: column;width: 14vw;margin-right: 1.5vw">
            <div style="display: flex;flex-direction: column;height: 30vh;margin-left: 0.5vw;margin-bottom: 2vh;"
                 class="back">
              <div
                  style="display: flex;justify-content: space-between;width: 12vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                  class="biaotou">
                <div style="vertical-align: middle;align-items: center;display: flex;">
                  <div style="display: flex;align-items: baseline;height: 100%;margin-left: 25%;" class="biaotouqian">
                    <el-image :src="require('@/assets/img/qianbiao.png')"
                              style="width: 0.6vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                  </div>
                  <div
                      style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;text-align: center;width: 100%;height: 100%;display: flex;">
                    直升机
                  </div>
                </div>
              </div>
              <div>
                <div class="formaction">
                  <div class="text">航速/km/h</div>
                  <div class="inputDiv">
                    <el-input v-model="form.Hel_v" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">高度/m</div>
                  <div class="inputDiv">
                    <el-input v-model="form.Hel_h" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">方位/°</div>
                  <div class="inputDiv">
                    <el-input v-model="form.Hel_B" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">攻击距离/m</div>
                  <div class="inputDiv">
                    <el-input v-model="form.Hel_D" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">目指角度误差/°</div>
                  <div class="inputDiv">
                    <el-input v-model="form.Err_theta" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">目指距离误差/m</div>
                  <div class="inputDiv">
                    <el-input v-model="form.Err_D" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
              </div>
            </div>


            <div style="display: flex;flex-direction: column;height: 20vh;margin-left: 0.5vw;margin-bottom: 2vh;"
                 class="back">
              <div
                  style="display: flex;justify-content: space-between;width: 12vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                  class="biaotou">
                <div style="vertical-align: middle;align-items: center;display: flex;">
                  <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                    <el-image :src="require('@/assets/img/qianbiao.png')"
                              style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                  </div>
                  <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">导弹弹道</div>
                </div>
              </div>
              <div>
                <div class="xuanzhongbeijing" tabindex="0">
                  <div class="formaction">
                    <div class="text">相对方位/°</div>
                    <div class="inputDiv">
                      <el-input v-model="form.fangwei" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                style="background-color: lightsalmon;" readonly="true"></el-input>
                    </div>
                  </div>
                </div>
                <div class="xuanzhongbeijing" tabindex="0">
                  <div class="formaction">
                    <div class="text">相对距离/m</div>
                    <div class="inputDiv">
                      <el-input v-model="form.juli" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                style="background-color: lightsalmon;" readonly="true"></el-input>
                    </div>
                  </div>
                </div>
                <div class="xuanzhongbeijing" tabindex="0">
                  <div class="formaction">
                    <div class="text">速度/Ma</div>
                    <div class="inputDiv">
                      <el-input v-model="form.V_missle" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                </div>
                <div class="xuanzhongbeijing" tabindex="0">
                  <div class="formaction">
                    <div class="text">最大航程/km</div>
                    <div class="inputDiv">
                      <el-input v-model="form.Mis_hc" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div style="display: flex;flex-direction: column;height: 13.5vh;margin-left: 0.5vw;margin-bottom: 1vh;"
                 class="back1">
              <div
                  style="display: flex;justify-content: space-between;width: 12vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                  class="biaotou">
                <div style="vertical-align: middle;align-items: center;display: flex;">
                  <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                    <el-image :src="require('@/assets/img/qianbiao.png')"
                              style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                  </div>
                  <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">火控参数</div>
                </div>
              </div>
              <div>
                <div class="xuanzhongbeijing" tabindex="0">
                  <div class="formaction">
                    <div class="text">射击点选择</div>
                    <div style="width: 4vw;text-align: left;color: #fff;height: 2.5vh;" @click="showOptions"
                         @focus="onFocus1" @blur="onBlur1" tabindex="0">
                      <div class="xuanzexiala" style="display: flex;width: 100%;height: 100%;position: relative;">
                        <img :src="require('@/assets/img/graphInput.png')"
                             style="position: absolute;z-index: 99;width:100%;height: 80%;">
                        <div class="selected-option">
                          {{ this.form.Mis_MZD || '' }}
                        </div>
                        <img :src="require('@/assets/img/graphDown.png')"
                             style="position: absolute;z-index: 99;width: 13%;height: 100%;object-fit: contain;right: 0.2vw;top: 0;"
                             v-if="typePic1 == 0">
                        <img :src="require('@/assets/img/graphUp.png')"
                             style="position: absolute;z-index: 99;width: 13%;height: 100%;object-fit: contain;right: 0.2vw;top: 0;"
                             v-if="typePic1 == 1">
                        <!-- <el-image :src="require('@/assets/img/xialajiantou.png')"
                          style="display: flex;align-items: center;"></el-image> -->
                      </div>
                    </div>
                    <ul v-if="showOptions2" class="options">
                      <li v-for="(option, index) in mzdList" :key="index" @click="selectOption2(option)">
                        {{ option.label }}
                      </li>
                    </ul>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">反应时间/s</div>
                  <div class="inputDiv">
                    <el-input v-model="form.Time_fanying" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <!-- <div class="formaction3">
                  <div class="text3">反应时间/s</div>
                  <div class="inputDiv">
                    <el-input v-model="form.Time_fanying" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div> -->
              </div>
            </div>
          </div>
          <div style="display: flex;flex-direction: column;width: 31vw;">
            <div style="display: flex;margin-bottom: 2vh">
              <div class="back1"
                   style="height: 30vh;display: flex;flex-direction: column;width: 14vw;margin-right: 1.5vw;">
                <div
                    style="display: flex;justify-content: space-between;width: 12.5vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                    class="biaotou">
                  <div style="vertical-align: middle;align-items: center;display: flex;">
                    <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                      <el-image :src="require('@/assets/img/qianbiao.png')"
                                style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                    </div>
                    <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">快艇</div>
                  </div>
                </div>
                <div style="display: flex;flex-direction: column;justify-content:space-between;">
                  <div class="xuanzhongbeijing" tabindex="0">
                    <div class="formaction">
                      <div class="text2">初始位置x/m</div>
                      <div class="inputDiv">
                        <el-input v-model="form.KT_x0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                      </div>
                    </div>
                  </div>
                  <div class="formaction">
                    <div class="text2">初始位置y/m</div>
                    <div class="inputDiv">
                      <el-input v-model="form.KT_y0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                  <div class="formaction">
                    <div class="text2">初始航向/°</div>
                    <div class="inputDiv">
                      <el-input v-model="form.KT_H0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                  <div class="formaction">
                    <div class="text2">初始航速/m</div>
                    <div class="inputDiv">
                      <el-input v-model="form.KT_v0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                  <div class="formaction">
                    <div class="text2">对空攻击距离/m</div>
                    <div class="inputDiv">
                      <el-input v-model="form.KT_AT_hel" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                  <div class="formaction">
                    <div class="text1" style="width: 7vw;">机动</div>
                    <div style="display: flex;align-items: center;justify-content: center;">
                      <el-checkbox v-model="form.checkedHX">&nbsp;航向</el-checkbox>
                      <el-checkbox v-model="form.checkedHS">&nbsp;航速</el-checkbox>
                    </div>
                  </div>
                  <div class="formaction" v-if="form.checkedHS == true">
                    <div class="text2">机动速度/kn</div>
                    <div class="inputDiv">
                      <el-input v-model="form.Jd_Sd" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                </div>
              </div>
              <div class="back1"
                   style="height: 30vh;display: flex;flex-direction: column;width: 14vw;margin-right: 1.5vw;">
                <div
                    style="display: flex;justify-content: space-between;width: 12.5vw;margin-bottom: 2vh;margin-top: 1vh;margin-left: 1vw;"
                    class="biaotou">
                  <div style="vertical-align: middle;align-items: center;display: flex;">
                    <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                      <el-image :src="require('@/assets/img/qianbiao.png')"
                                style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                    </div>
                    <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">仿真控制</div>
                  </div>
                </div>
                <div style="display: flex;flex-direction: column;justify-content:space-between;">
                  <div class="xuanzhongbeijing" tabindex="0">
                    <div class="formaction">
                      <div class="text2">仿真步长/s</div>
                      <div class="inputDiv">
                        <el-input v-model="form.delta_t" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                      </div>
                    </div>
                  </div>
                  <div class="formaction">
                    <div class="text2">仿真次数</div>
                    <div class="inputDiv">
                      <el-input v-model="form.num_sumli" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                  <div class="formaction4">
                    <el-button class="button2" @click="test">载入测试值</el-button>
                  </div>
                  <div class="formaction4">
                    <el-button class="button2" @click="dataInitialize">数据初始化</el-button>
                  </div>
                  <div class="formaction5">
                    <el-button class="button3" @click="submitForm">计算</el-button>
                    <el-button class="button3" @click="finishComp">结束计算</el-button>
                  </div>
                  <div class="formaction5">
                    <!--                    <el-button class="button3" @click="zanting = 0">继续</el-button>-->
                    <el-button class="button3" @click="togglePause">
                      {{ zanting === 0 ? '暂停' : '继续' }}
                    </el-button>
                    <el-button class="button3" @click="clearImage">清除数据</el-button>
                  </div>
                </div>
              </div>
            </div>
            <div style="display: flex;margin-bottom: 2vh;">
              <div style="display: flex;margin-bottom: 2vh;flex-direction: column;width: 14vw;margin-right: 1.5vw;">
                <div style="display: flex;flex-direction: column;height: 20vh;margin-bottom: 2vh;" class="back1">
                  <div
                      style="display: flex;justify-content: space-between;width: 12.5vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                      class="biaotou">
                    <div style="vertical-align: middle;align-items: center;display: flex;">
                      <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                        <el-image :src="require('@/assets/img/qianbiao.png')"
                                  style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                      </div>
                      <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">导弹导引头</div>
                    </div>
                  </div>
                  <div>
                    <div class="xuanzhongbeijing" tabindex="0">
                      <div class="formaction">
                        <div class="text2">波段/mm</div>
                        <div class="inputDiv">
                          <el-input v-model="form.Mis_D_bc" autocomplete="off" @focus="onFocus"
                                    @blur="onBlur"></el-input>
                        </div>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">搜索扇面/°</div>
                      <div class="inputDiv">
                        <el-input v-model="form.Mis_D_Lamda" autocomplete="off" @focus="onFocus"
                                  @blur="onBlur"></el-input>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">扇面误差/°</div>
                      <div class="inputDiv">
                        <el-input v-model="form.Mis_D_Lamda_err" autocomplete="off" @focus="onFocus"
                                  @blur="onBlur"></el-input>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">导引头开机距离/m</div>
                      <div class="inputDiv">
                        <el-input v-model="form.KT_DT_missle" autocomplete="off" @focus="onFocus"
                                  @blur="onBlur"></el-input>
                      </div>
                    </div>
                    <!-- <div class="formaction">
                      <div class="text2">脉冲宽度/us</div>
                      <div class="inputDiv">
                        <el-input v-model="form.Tao" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                      </div>
                    </div> -->
                  </div>
                </div>
                <div style="display: flex;flex-direction: column;height: 13.5vh;margin-bottom: 1vh;" class="back1">
                  <div
                      style="display: flex;justify-content: space-between;width: 12.5vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                      class="biaotou">
                    <div style="vertical-align: middle;align-items: center;display: flex;">
                      <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                        <el-image :src="require('@/assets/img/qianbiao.png')"
                                  style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                      </div>
                      <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">环境参数</div>
                    </div>
                  </div>
                  <div>
                    <div class="xuanzhongbeijing" tabindex="0">
                      <div class="formaction">
                        <div class="text2">海况等级</div>
                        <div class="inputDiv">
                          <el-input v-model="form.Sea_hk" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">降水量/mm</div>
                      <div class="inputDiv">
                        <el-input v-model="form.Rain_jiangyu" autocomplete="off" @focus="onFocus"
                                  @blur="onBlur"></el-input>
                      </div>
                    </div>
                  </div>
                </div>

              </div>
              <div style="display: flex;flex-direction: column;">
                <div class="back1" style="height: 35.5vh;display: flex;flex-direction: column;width: 14vw;">
                  <div
                      style="display: flex;justify-content: space-between;width: 12.5vw;margin-bottom: 2vh;margin-top: 1vh;margin-left: 1vw;"
                      class="biaotou">
                    <div style="vertical-align: middle;align-items: center;display: flex;">
                      <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                        <el-image :src="require('@/assets/img/qianbiao.png')"
                                  style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                      </div>
                      <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">结果输出</div>
                    </div>
                  </div>
                  <div style="display: flex;flex-direction: column;justify-content:space-between;">
                    <div class="xuanzhongbeijing" tabindex="0">
                      <div class="formaction">
                        <div class="text2">导弹航程/m</div>
                        <div class="inputDiv">
                          <el-input v-model="form.Mis_sc" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                    style="background-color: lightsalmon;" readonly="true"></el-input>
                        </div>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">导弹高度/m</div>
                      <div class="inputDiv">
                        <el-input v-model="form.Mis_gd" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  style="background-color: lightsalmon;" readonly="true"></el-input>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">波门上限/m</div>
                      <div class="inputDiv">
                        <el-input v-model="form.Mis_Serch_up" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  style="background-color: lightsalmon;" readonly="true"></el-input>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">波门下限/m</div>
                      <div class="inputDiv">
                        <el-input v-model="form.Mis_Serch_down" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  style="background-color: lightsalmon;" readonly="true"></el-input>
                      </div>
                    </div>
                    <div class="formaction4" style="margin-top: 1vh;">
                      <div class="inputDiv">
                        <el-button @click="submitForm1">评估</el-button>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">击水概率</div>
                      <div class="inputDiv">
                        <el-input v-model="form.jiShuiResult" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  style="background-color: lightsalmon;" readonly="true"></el-input>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">命中概率</div>
                      <div class="inputDiv">
                        <el-input v-model="result" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  style="background-color: lightsalmon;" readonly="true"></el-input>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div style="display: flex;flex-direction: column;">
            <div class="back4" style="display: flex;">
              <div style="height: 96%;width: 100%;margin-top: 1%;display: flex;justify-content: center;">
                <div id="missileChart" style="width: 400px; height: 300px;margin-top: 0.2vw;"></div>
              </div>
            </div>
            <div class="back4" style="display: flex;flex-direction: column;height: 32.5vh;">
              <div
                  style="display: flex;justify-content: space-between;width: 26vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                  class="biaotou">
                <div style="vertical-align: middle;align-items: center;display: flex;">
                  <div style="display: flex;align-items: baseline;height: 100%;margin-left: 25%;" class="biaotouqian">
                    <el-image :src="require('@/assets/img/qianbiao.png')"
                              style="width: 0.6vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;"/>
                  </div>
                  <div
                      style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;text-align: center;width: 100%;height: 100%;display: flex;">
                    消息呈现栏
                  </div>
                </div>
              </div>
              <div class="textArea">
                <el-input type="textarea" :rows="2" v-model="resultStr" readonly>
                </el-input>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>


  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  data() {
    return {
      showBig: false,
      zanting: 0,
      zantingList: [],
      currentImage: null,
      socket: null,
      dataFinal1: {
        jsId: null,
        jsResult: {},
        allImg: null,
      },
      showOptions2: false,
      typePic1: false,
      result: 0,
      resultStr: "",
      mzdList: [{
        id: 1,
        label: "当前点",
        value: 0,
      },
        {
          id: 2,
          label: "前置点",
          value: 1,
        }],
      form: {
        Hel_D: 0,
        Hel_B: 0,
        Hel_v: 0,
        Hel_h: 0,
        Err_theta: 0,
        Err_D: 0,
        KT_x0: 0,
        KT_y0: 0,
        KT_v0: 0,
        KT_H0: 0,
        KT_DT_missle: 0,
        KT_AT_hel: 0,
        Mis_Serch_up: 0,
        Mis_Serch_down: 0,
        jiShuiResult: 0,
        V_missle: 0,
        checkedHX: false,
        checkedHS: false,
        Jd_Sd: 0,
        Mis_hc: 0,
        Mis_MZD: '当前点',
        Time_fanying: 0,
        Mis_sc: 0,
        Mis_gd: 0,
        Mis_D_Lamda: 0,
        Mis_D_Lamda_err: 0,
        Tao: 0,
        Mis_D_bc: 0,
        Sea_hk: 0,
        Rain_jiangyu: 0,
        delta_t: 0,
        num_sumli: 0,
        result: 0,
      },
      form1: {},


      chart: null,
      // 存储图形元素引用
      circle1Ref: null,
      circle2Ref: null,
      pointKTRef: null,
      linesRef: [],
      currentSeries: [],
      playbackTimeoutId: null,
      processingIndex: 0,     // 当前已处理到第几个
    };
  },
  beforeDestroy() {
    if (this.socket) {
      this.socket.close();
    }
  },
  watch: {
    // 监听 zanting 变化：从暂停到继续时，检查是否有待处理数据
    zanting(newVal, oldVal) {
      // 情况1：从运行 → 暂停
      if (oldVal === 0 && newVal === 1) {
        console.log('已暂停，当前处理进度:', this.processingIndex);
        if (this.playbackTimeoutId) {
          clearTimeout(this.playbackTimeoutId);
          this.playbackTimeoutId = null;
          console.log('已暂停，当前处理进度:', this.processingIndex);
        }
        return;
      }

      // 情况2：从暂停 → 继续
      if (oldVal === 1 && newVal === 0) {
        if (this.zantingList.length === 0) return;

        console.log('继续绘图，从索引', this.processingIndex, '开始');

        const delay = 50;

        const processNext = () => {
          if (this.processingIndex < this.zantingList.length) {
            const item = this.zantingList[this.processingIndex];
            this.batchProcessData([item]);
            this.processingIndex++;

            this.playbackTimeoutId = setTimeout(processNext, delay);
          } else {
            this.playbackTimeoutId = null;
          }
        };

        processNext();
      }
    },
    // 原来的 zantingList 监听
    zantingList: {
      handler(newList) {
        if (this.zanting === 0 && newList.length > 0) {
          this.batchProcessData(newList);
          this.zantingList = [];
        }
      },
      deep: true
    }
  },

  created() {

    // 连接 FastAPI WebSocket
    this.socket = new WebSocket('ws://127.0.0.1:9086/ws');


    this.socket.onopen = () => {
      console.log('WebSocket 已连接');
    };

    // this.socket.onmessage = (event) => {
    //   const data = JSON.parse(event.data);
    //   this.response = data;
    // };

    this.socket.onclose = (e) => {
      console.error("连接关闭详情:", e);
      console.error("关闭代码:", e.code);      // WebSocket 关闭状态码（如 1006 异常关闭）
      console.error("关闭原因:", e.reason);    // 服务器返回的关闭原因
      console.error("是否干净关闭:", e.wasClean); // 是否正常关闭
    };

    this.socket.onerror = (err) => {
      console.error('WebSocket 错误:', err);
    };


  },
  methods: {
    togglePause() {
      this.zanting = this.zanting === 0 ? 1 : 0;
    },
    //这是新的
    initChart() {
      this.chart = echarts.init(document.getElementById('missileChart'), null, {
        renderer: 'canvas',
        devicePixelRatio: 2
      });

      // 初始化动态范围
      this.currentXRange = { min: -10000, max: 8000 };
      this.currentYRange = { min: -6000, max: 7000 };

      const option = {
        xAxis: {
          type: 'value',
          min: this.currentXRange.min,
          max: this.currentXRange.max,
          name: 'X(m)',
          nameLocation: 'end',
          axisLine: { show: true },
          axisLabel: {
            show: true,
            fontSize: 10
          },
          nameGap: 5
        },
        yAxis: {
          type: 'value',
          min: this.currentYRange.min,
          max: this.currentYRange.max,
          name: 'Y(m)',
          nameLocation: 'end',
          axisLine: { show: true },
          axisLabel: {
            show: true,
            fontSize: 10
          },
          nameGap: 5
        },
        grid: {
          show: true,
          borderWidth: 0,
          backgroundColor: '#f8f9fa',
          left: 15,
          right: 40,
          top: 30,
          bottom: 20,
          containLabel: true
        },
        tooltip: {
          trigger: 'item',
          formatter: function (params) {
            if (params.componentType === 'series') {
              return `${params.seriesName}<br/>坐标: (${params.data[0].toFixed(2)}, ${params.data[1].toFixed(2)})`;
            }
            return params.name;
          }
        },
        animation: false,
        series: []
      };

      this.chart.setOption(option);
    },

// 检测并更新坐标轴范围
    // 检测并更新坐标轴范围
    updateAxisRange(dataList) {
      let needsUpdate = false;
      const padding = 1000; // 边距，确保数据不会紧贴边界

      // 临时变量存储检测到的新范围
      let newXMin = this.currentXRange.min;
      let newXMax = this.currentXRange.max;
      let newYMin = this.currentYRange.min;
      let newYMax = this.currentYRange.max;

      dataList.forEach(data1 => {
        if (data1.type === 'chart_update') {
          // 处理点数据
          if (data1.part === 'point') {
            const xValues = Array.isArray(data1.x) ? data1.x : [data1.x];
            const yValues = Array.isArray(data1.y) ? data1.y : [data1.y];

            xValues.forEach(x => {
              if (x < this.currentXRange.min + padding) {
                newXMin = Math.floor(x - padding);
                needsUpdate = true;
              } else if (x > this.currentXRange.max - padding) {
                newXMax = Math.ceil(x + padding);
                needsUpdate = true;
              }
            });

            yValues.forEach(y => {
              if (y < this.currentYRange.min + padding) {
                newYMin = Math.floor(y - padding);
                needsUpdate = true;
              } else if (y > this.currentYRange.max - padding) {
                newYMax = Math.ceil(y + padding);
                needsUpdate = true;
              }
            });
          }

          // 处理圆形数据
          else if (data1.part === 'circle' || data1.part === 'circleSm') {
            const centerX = data1.xx;
            const centerY = data1.yy;
            const radius = Math.max(data1.r1 || 0, data1.r2 || 0);

            // 检查圆形边界
            const circleXMin = centerX - radius;
            const circleXMax = centerX + radius;
            const circleYMin = centerY - radius;
            const circleYMax = centerY + radius;

            if (circleXMin < this.currentXRange.min + padding) {
              newXMin = Math.floor(circleXMin - padding);
              needsUpdate = true;
            } else if (circleXMax > this.currentXRange.max - padding) {
              newXMax = Math.ceil(circleXMax + padding);
              needsUpdate = true;
            }

            if (circleYMin < this.currentYRange.min + padding) {
              newYMin = Math.floor(circleYMin - padding);
              needsUpdate = true;
            } else if (circleYMax > this.currentYRange.max - padding) {
              newYMax = Math.ceil(circleYMax + padding);
              needsUpdate = true;
            }

            // 检测扇面线的边界（如果有扇面数据）
            if (data1.part === 'circleSm' && data1.line1 && data1.line2 && data1.line3) {
              const sectorLines = [data1.line1, data1.line2, data1.line3];

              sectorLines.forEach(line => {
                if (line && line.x && line.y) {
                  // 检测扇面线的所有点
                  line.x.forEach((x, index) => {
                    const y = line.y[index];

                    if (x < this.currentXRange.min + padding) {
                      newXMin = Math.floor(x - padding);
                      needsUpdate = true;
                    } else if (x > this.currentXRange.max - padding) {
                      newXMax = Math.ceil(x + padding);
                      needsUpdate = true;
                    }

                    if (y < this.currentYRange.min + padding) {
                      newYMin = Math.floor(y - padding);
                      needsUpdate = true;
                    } else if (y > this.currentYRange.max - padding) {
                      newYMax = Math.ceil(y + padding);
                      needsUpdate = true;
                    }
                  });
                }
              });
            }
          }
        }
      });

      // 如果需要更新，则应用新的范围
      if (needsUpdate) {
        this.currentXRange = { min: newXMin, max: newXMax };
        this.currentYRange = { min: newYMin, max: newYMax };

        this.chart.setOption({
          xAxis: {
            min: newXMin,
            max: newXMax
          },
          yAxis: {
            min: newYMin,
            max: newYMax
          }
        });
      }

      return needsUpdate;
    },

    // 颜色映射
    getColor(colorCode) {
      const colorMap = {
        'r': '#ff4d4f',
        'k': '#000000',
        'b': '#1890ff',
        'c': '#13c2c2',
        'g': '#52c41a',
        'm': '#eb2f96',
        'y': '#fadb14'
      };
      return colorMap[colorCode] || colorCode;
    },
    drawCircle(centerX, centerY, radius, color, lineStyle = 'solid', name = 'circle') {
      const points = [];
      for (let i = 0; i <= 360; i += 5) {
        const angle = (i * Math.PI) / 180;
        const x = centerX + radius * Math.cos(angle);
        const y = centerY + radius * Math.sin(angle);
        points.push([x, y]);
      }

      const series = {
        name: name, // 如 'kill-radius', 'detect-radius'
        type: 'line',
        data: points,
        symbol: 'none',
        lineStyle: {
          color: this.getColor(color),
          type: lineStyle,
          width: 1
        },
        itemStyle: {
          color: this.getColor(color)
        },
        animation: false,
        large: true,
        progressive: 200,
        progressiveThreshold: 1000
      };

      return this.addSeries(series);
    },
    deleteCircle() {
      // 删除具有特定名称的圆
      this.removeSeriesByName('探测');
      this.removeSeriesByName('攻击');

      // 可选：清空引用（如果仍需保留标记）
      this.circle1Ref = null;
      this.circle2Ref = null;

      console.log("已删除所有圆形");
    },
    // 根据 series 名称移除
    removeSeriesByName(seriesName) {
      const option = this.chart.getOption();
      const newSeries = option.series.filter(s => s.name !== seriesName);
      if (newSeries.length < option.series.length) {
        this.chart.setOption({
          ...option,
          series: newSeries
        }, true);
        return true; // 成功删除
      }
      return false;
    },

    // 添加系列到图表
    addSeries(series) {
      const currentOption = this.chart.getOption();
      const seriesIndex = currentOption.series.length;

      currentOption.series.push(series);
      this.chart.setOption(currentOption);

      return seriesIndex;
    },

    batchProcessData(dataList) {
      // 先检测并更新坐标轴范围
      this.updateAxisRange(dataList);

      const points = [];
      const circles = [];
      const circleSms = [];
      const others = [];

      dataList.forEach(data1 => {
        if (data1.type === 'chart_update') {
          if (data1.part === 'point') {
            points.push(data1);
          } else if (data1.part === 'circle') {
            circles.push(data1);
          } else if (data1.part === 'circleSm') {
            circleSms.push(data1);
          }
        } else {
          others.push(data1);
        }
      });

      // 1. 批量绘制轨迹点（保留历史）
      if (points.length > 0) {
        this.batchDrawPoints(points);
      }

      // 2. 处理大圆：删除旧的，画最新的
      if (circles.length > 0) {
        const lastCircle = circles[circles.length - 1];
        this.deleteCircle();
        this.drawCircle(lastCircle.xx, lastCircle.yy, lastCircle.r1, "red", "solid", "探测");
        this.drawCircle(lastCircle.xx, lastCircle.yy, lastCircle.r2, "blue", "dashed", "攻击");
      }

      // 3. 处理带扇面的小圆
      if (circleSms.length > 0) {
        const lastCircleSm = circleSms[circleSms.length - 1];
        this.deleteCircle();
        this.drawCircle(lastCircleSm.xx, lastCircleSm.yy, lastCircleSm.r1, "red", "solid", "探测");
        this.drawCircle(lastCircleSm.xx, lastCircleSm.yy, lastCircleSm.r2, "blue", "dashed", "攻击");

        // 同时绘制扇面线
        this.drawSectorLines(lastCircleSm.line1, lastCircleSm.line2, lastCircleSm.line3);
      }

      // 4. 其他状态更新
      if (others.length > 0) {
        const lastOther = others[others.length - 1];
        this.processOtherData(lastOther);
      }

      // 5. 更新表单
      const lastData = dataList[dataList.length - 1];
      this.updateFormData(lastData);
    },

    drawSectorLines(line1Data, line2Data, line3Data) {
      this.linesRef.forEach(name => this.removeSeriesByName(name));
      this.linesRef = [];

      const addLine = (data, legendName, showInLegend = true) => {
        const points = data.x.map((x, i) => [x, data.y[i]]);
        const series = {
          id: `sector-${Date.now()}-${Math.random().toString(36).substr(2, 5)}`,
          name: legendName,
          type: 'line',
          data: points,
          symbol: 'none',
          lineStyle: {
            color: '#efd209',
            type: '-.',
            width: 2
          },
          itemStyle: {
            color: '#efd209' // ✅ 关键：必须设置，否则图例填充可能为空
          },
          animation: false
        };

        // 如果不想出现在图例中，可以设置：
        if (!showInLegend) {
          series.legendHoverLink = false;
          series.silent = true;
        }

        this.addSeries(series);
        this.linesRef.push(legendName);
      };

      addLine(line1Data, '导引头', true);   // 图例显示
      addLine(line2Data, '导引头', false);      // 不显示
      addLine(line3Data, '导引头', false);     // 不显示
    },

    batchDrawPoints(points) {
      points.forEach((point, idx) => {
        const color = point.color === 'ro' ? 'red' : 'blue';
        const data = Array.isArray(point.x)
            ? point.x.map((xi, i) => [xi, point.y[i]])
            : [[point.x, point.y]];

        const series = {
          id: `track-${Date.now()}-${idx}`,     // 用于删除
          name: '导弹轨迹',                      // 统一图例名
          type: 'line',
          data: data,
          symbol: 'circle',
          symbolSize: 4,
          lineStyle: {
            color: color,
            width: 1
          },
          itemStyle: {
            color: color
          },
          animation: false
        };

        this.addSeries(series);
      });
    },



    processOtherData(data1) {
      if (data1.type === 'result_update') {
        this.resultStr = data1.result;
        if (data1.jiShuiResult != 0) {
          this.form.jiShuiResult = data1.jiShuiResult;
        }
      } else if (data1.type === 'state_update') {
        this.resultStr = data1.result;
      } else if (data1.type === 'average_update') {
        this.result = data1.str[0];
        this.form.jiShuiResult = data1.str[1];
      } else if (data1.type === 'process') {
        if (data1.flag_mz == 1) {
          this.resultStr = "第" + (data1.numstr + 1) + "次运行，导弹命中快艇，用时" + data1.str + "秒";
        } else {
          this.resultStr = "第" + (data1.numstr + 1) + "次运行，导弹未命中快艇，用时" + data1.str + "秒";
        }
      }
    },

    updateFormData(data1) {
      if (data1.type === 'chart_update' || data1.type === 'result_update') {
        this.currentImage = data1.image || this.currentImage;
        if (data1.result && data1.result !== "") {
          this.resultStr = data1.result;
        }

        this.form.Mis_sc = data1.Mis_sc || this.form.Mis_sc;
        this.form.Mis_gd = data1.Mis_gd || this.form.Mis_gd;
        this.form.Mis_Serch_up = data1.Mis_Serch_up || this.form.Mis_Serch_up;
        this.form.Mis_Serch_down = data1.Mis_Serch_down || this.form.Mis_Serch_down;
        this.form.fangwei = data1.FangWei || this.form.fangwei;
        this.form.juli = data1.Xiangduijuli || this.form.juli;
      }
    },


    finishComp() {
      // 1. 设置 zanting = 1，触发暂停逻辑
      this.zanting = 1;

      // 2. 确保清除当前播放定时器（双重保险）
      if (this.playbackTimeoutId) {
        clearTimeout(this.playbackTimeoutId);
        this.playbackTimeoutId = null;
      }

      console.log('计算已结束，系统处于暂停状态');
    },




    showBigInfo() {
      this.showBig = true;

    },
    clearImage() {
      // 1. 清除定时器
      if (this.playbackTimeoutId) {
        clearTimeout(this.playbackTimeoutId);
        this.playbackTimeoutId = null;
      }

      // 2. 清空数据
      this.zantingList = [];
      this.processingIndex = 0;
      this.zanting = 1;

      // 3. ✅ 获取当前 option 中的 xAxis, yAxis 等
      if (this.chart) {
        const currentOption = this.chart.getOption();

        // 构造一个只包含基础结构 + 空 series 的 option
        const cleanOption = {
          title: currentOption.title,
          xAxis: currentOption.xAxis,
          yAxis: currentOption.yAxis,
          grid: currentOption.grid,
          legend: currentOption.legend,
          tooltip: currentOption.tooltip,
          series: []  // 明确清空
        };

        // ✅ 使用 notMerge: true，强制替换
        this.chart.setOption(cleanOption, true);
      }
      console.log('所有数据和图形已清除');
      this.zanting = 0;

      // 可选：提示用户
      // this.$message.success('数据已清除');
      this.currentImage = "";
      this.form.Hel_D = 0;
      this.form.Hel_B = 0;
      this.form.Hel_v = 0;
      this.form.Hel_h = 0;
      this.form.Err_theta = 0;
      this.form.Err_D = 0;
      this.form.KT_x0 = 0;
      this.form.KT_y0 = 0;
      this.form.KT_v0 = 0;
      this.form.KT_H0 = 0;
      this.form.KT_DT_missle = 0;
      this.form.KT_AT_hel = 0;
      this.form.V_missle = 0;
      this.form.Mis_hc = 0;
      this.form.checkedHS = false;
      this.form.checkedHX = false;
      this.form.Jd_Sd = 0;
      this.form.Mis_D_Lamda = 0;
      this.form.Mis_D_Lamda_err = 0;
      this.form.Tao = 0;
      this.form.Mis_MZD = "当前点";
      this.form.Time_fanying = 0;
      this.form.Mis_D_bc = 0;
      this.form.Sea_hk = 0;
      this.form.Rain_jiangyu = 0;
      this.form.delta_t = 0;
      this.form.num_sumli = 0;
      this.resultStr = "";
      this.form.Mis_sc = 0;
      this.form.Mis_gd = 0;
      this.form.jiShuiResult = 0;
      this.form.Mis_Serch_up = 0;
      this.form.Mis_Serch_down = 0;
      this.form.fangwei = 0;
      this.form.juli = 0;


      var dataFinal = {
        // 直升机参数
        "Hel_D": this.form.Hel_D,
        "Hel_B": this.form.Hel_B,
        "Hel_v": this.form.Hel_v,
        "Hel_h": this.form.Hel_h,

        // 误差参数
        "Err_theta": this.form.Err_theta,
        "Err_D": this.form.Err_D,

        // 快艇参数
        "KT_x0": this.form.KT_x0,
        "KT_y0": this.form.KT_y0,
        "KT_v0": this.form.KT_v0,
        "KT_H0": this.form.KT_H0,
        "KT_DT_missle": this.form.KT_DT_missle,
        "KT_AT_hel": this.form.KT_AT_hel,
        "checkedHX": this.form.checkedHX,
        "checkedHS": this.form.checkedHS,
        "Jd_Sd": this.form.Jd_Sd,

        // 导弹参数
        "V_missle": this.form.V_missle,
        "Mis_hc": this.form.Mis_hc,
        "Mis_D_Lamda": this.form.Mis_D_Lamda,
        "Mis_D_Lamda_err": this.form.Mis_D_Lamda_err,
        "Mis_D_bc": this.form.Mis_D_bc,
        "Tao": this.form.Tao,

        //火控参数
        "Mis_MZD": this.form.Mis_MZD,
        "Time_fanying": this.form.Time_fanying,

        // 环境参数
        "Sea_hk": this.form.Sea_hk,
        "Rain_jiangyu": this.form.Rain_jiangyu,

        // 其他参数
        "delta_t": this.form.delta_t,
        "num_sumli": 0,

      };
      if (dataFinal.Mis_MZD == "当前点") {
        dataFinal.Mis_MZD = 1;
      } else {
        dataFinal.Mis_MZD = 0;
      }
      if (this.form.checkedHS) {
        dataFinal.checkedHS = 1;
      } else {
        dataFinal.checkedHS = 0;
      }
      if (this.form.checkedHX) {
        dataFinal.checkedHX = 1;
      } else {
        dataFinal.checkedHX = 0;
      }
      this.connectWebSocket(dataFinal)
    },
    dataInitialize() {
      this.form.Hel_D = this.form1.Hel_D;
      this.form.Hel_B = this.form1.Hel_B;
      this.form.Hel_v = this.form1.Hel_v;
      this.form.Hel_h = this.form1.Hel_h;
      this.form.Err_theta = this.form1.Err_theta;
      this.form.Err_D = this.form1.Err_D;
      this.form.KT_x0 = this.form1.KT_x0;
      this.form.KT_y0 = this.form1.KT_y0;
      this.form.KT_v0 = this.form1.KT_v0;
      this.form.KT_H0 = this.form1.KT_H0;
      this.form.checkedHS = this.form1.checkedHS;
      this.form.checkedHX = this.form1.checkedHX;
      this.form.Jd_Sd = this.form1.Jd_Sd;
      this.form.KT_DT_missle = this.form1.KT_DT_missle;
      this.form.KT_AT_hel = this.form1.KT_AT_hel;
      this.form.V_missle = this.form1.V_missle;
      this.form.Mis_hc = this.form1.Mis_hc;
      this.form.Mis_D_Lamda = this.form1.Mis_D_Lamda;
      this.form.Mis_D_Lamda_err = this.form1.Mis_D_Lamda_err;
      this.form.Tao = this.form1.Tao;
      this.form.Mis_MZD = this.form1.Mis_MZD;
      this.form.Time_fanying = this.form1.Time_fanying;
      this.form.Mis_D_bc = this.form1.Mis_D_bc;
      this.form.Sea_hk = this.form1.Sea_hk;
      this.form.Rain_jiangyu = this.form1.Rain_jiangyu;
      this.form.delta_t = this.form1.delta_t;
      this.form.num_sumli = this.form1.num_sumli;
    },
    onFocus(event) {
      const parentDiv = event.target.closest('.formaction');
      if (parentDiv) {
        const imagePath = require('@/assets/img/xuanzhongduan.png');
        parentDiv.style.backgroundImage = `url(${imagePath})`;
        parentDiv.style.backgroundRepeat = "no-repeat";
        parentDiv.style.backgroundSize = "100%";
      }
    },
    onBlur(event) {
      const parentDiv = event.target.closest('.formaction');
      if (parentDiv) {
        parentDiv.style.backgroundImage = '';
      }
    },
    onFocus1(event) {
      const parentDiv = event.target.closest('.formaction1');
      if (parentDiv) {
        const imagePath = require('@/assets/img/xuanzhongchang.png');
        parentDiv.style.backgroundImage = `url(${imagePath})`;
        parentDiv.style.backgroundRepeat = "no-repeat";
        parentDiv.style.backgroundSize = "100%";
        parentDiv.style.backgroundPosition = "0 0.3vh";
      }
    },
    onBlur1(event) {
      const parentDiv = event.target.closest('.formaction1');
      if (parentDiv) {
        parentDiv.style.backgroundImage = '';
      }
    },
    showOptions() {
      this.showOptions2 = !this.showOptions2;
      this.showOptions3 = false;
      this.showOptions4 = false;
      this.typePic1 = !this.typePic1;
    },
    showOptions1() {
      this.showOptions3 = !this.showOptions3;
      this.showOptions2 = false;
      this.showOptions4 = false;
    },
    showOptions5() {
      this.showOptions4 = !this.showOptions4;
      this.showOptions2 = false;
      this.showOptions3 = false;
    },
    selectOption2(option) {
      this.form.Mis_MZD = option.label;
      this.typePic1 = false;
      this.showOptions2 = false;
    },
    selectOption3(option) {
      this.form.heli_type = option.value;
      this.showOptions3 = false;
    },
    selectOption4(option) {
      this.form.zjsb = option.value;
      this.showOptions4 = false;
    },
    submitForm() {
      this.zantingList = [];
      var dataFinal = {
        // 直升机参数
        "Hel_D": this.form.Hel_D,
        "Hel_B": this.form.Hel_B,
        "Hel_v": this.form.Hel_v,
        "Hel_h": this.form.Hel_h,

        // 误差参数
        "Err_theta": this.form.Err_theta,
        "Err_D": this.form.Err_D,

        // 快艇参数
        "KT_x0": this.form.KT_x0,
        "KT_y0": this.form.KT_y0,
        "KT_v0": this.form.KT_v0,
        "KT_H0": this.form.KT_H0,
        "KT_DT_missle": this.form.KT_DT_missle,
        "KT_AT_hel": this.form.KT_AT_hel,
        "checkedHX": this.form.checkedHX,
        "checkedHS": this.form.checkedHS,
        "Jd_Sd": this.form.Jd_Sd,

        // 导弹参数
        "V_missle": this.form.V_missle,
        "Mis_hc": this.form.Mis_hc,
        "Mis_D_Lamda": this.form.Mis_D_Lamda,
        "Mis_D_Lamda_err": this.form.Mis_D_Lamda_err,
        "Mis_D_bc": this.form.Mis_D_bc,
        "Tao": this.form.Tao,

        //火控参数
        "Mis_MZD": this.form.Mis_MZD,
        "Time_fanying": this.form.Time_fanying,

        // 环境参数
        "Sea_hk": this.form.Sea_hk,
        "Rain_jiangyu": this.form.Rain_jiangyu,

        // 其他参数
        "delta_t": this.form.delta_t,
        "num_sumli": 0,


      };
      if (dataFinal.Mis_MZD == "当前点") {
        dataFinal.Mis_MZD = 1;
      } else {
        dataFinal.Mis_MZD = 0;
      }
      if (this.form.checkedHS) {
        dataFinal.checkedHS = 1;
      } else {
        dataFinal.checkedHS = 0;
      }
      if (this.form.checkedHX) {
        dataFinal.checkedHX = 1;
      } else {
        dataFinal.checkedHX = 0;
      }
      this.connectWebSocket(dataFinal)

    },
    submitForm1() {
      var dataFinal2 = {
        // 直升机参数
        "Hel_D": this.form.Hel_D,
        "Hel_B": this.form.Hel_B,
        "Hel_v": this.form.Hel_v,
        "Hel_h": this.form.Hel_h,

        // 误差参数
        "Err_theta": this.form.Err_theta,
        "Err_D": this.form.Err_D,

        // 快艇参数
        "KT_x0": this.form.KT_x0,
        "KT_y0": this.form.KT_y0,
        "KT_v0": this.form.KT_v0,
        "KT_H0": this.form.KT_H0,
        "KT_DT_missle": this.form.KT_DT_missle,
        "KT_AT_hel": this.form.KT_AT_hel,
        "checkedHX": this.form.checkedHX,
        "checkedHS": this.form.checkedHS,
        "Jd_Sd": this.form.Jd_Sd,

        // 导弹参数
        "V_missle": this.form.V_missle,
        "Mis_hc": this.form.Mis_hc,
        "Mis_D_Lamda": this.form.Mis_D_Lamda,
        "Mis_D_Lamda_err": this.form.Mis_D_Lamda_err,
        "Mis_D_bc": this.form.Mis_D_bc,
        "Tao": this.form.Tao,

        //火控参数
        "Mis_MZD": this.form.Mis_MZD,
        "Time_fanying": this.form.Time_fanying,

        // 环境参数
        "Sea_hk": this.form.Sea_hk,
        "Rain_jiangyu": this.form.Rain_jiangyu,

        // 其他参数
        "delta_t": this.form.delta_t,
        "num_sumli": this.form.num_sumli,


      };
      if (dataFinal2.Mis_MZD == "当前点") {
        dataFinal2.Mis_MZD = 1;
      } else {
        dataFinal2.Mis_MZD = 0;
      }
      if (this.form.checkedHS) {
        dataFinal2.checkedHS = 1;
        dataFinal2.Jd_Sd = this.form.Jd_Sd;
      } else {
        dataFinal2.checkedHS = 0;
      }
      if (this.form.checkedHX) {
        dataFinal2.checkedHX = 1;
      } else {
        dataFinal2.checkedHX = 0;
      }
      this.connectWebSocket(dataFinal2)

    },
    connectWebSocket(dataFinal) {

      this.form1.Hel_D = this.form.Hel_D;
      this.form1.Hel_B = this.form.Hel_B;
      this.form1.Hel_v = this.form.Hel_v;
      this.form1.Hel_h = this.form.Hel_h;
      this.form1.Err_theta = this.form.Err_theta;
      this.form1.Err_D = this.form.Err_D;
      this.form1.KT_x0 = this.form.KT_x0;
      this.form1.KT_y0 = this.form.KT_y0;
      this.form1.KT_v0 = this.form.KT_v0;
      this.form1.KT_H0 = this.form.KT_H0;
      this.form1.checkedHS = this.form.checkedHS;
      this.form1.checkedHX = this.form.checkedHX;
      this.form1.Jd_Sd = this.form.Jd_Sd;
      this.form1.KT_DT_missle = this.form.KT_DT_missle;
      this.form1.KT_AT_hel = this.form.KT_AT_hel;
      this.form1.V_missle = this.form.V_missle;
      this.form1.Mis_hc = this.form.Mis_hc;
      this.form1.Mis_D_Lamda = this.form.Mis_D_Lamda;
      this.form1.Mis_D_Lamda_err = this.form.Mis_D_Lamda_err;
      this.form1.Tao = this.form.Tao;
      this.form1.Mis_MZD = this.form.Mis_MZD;
      this.form1.Time_fanying = this.form.Time_fanying;
      this.form1.Mis_D_bc = this.form.Mis_D_bc;
      this.form1.Sea_hk = this.form.Sea_hk;
      this.form1.Rain_jiangyu = this.form.Rain_jiangyu;
      this.form1.delta_t = this.form.delta_t;
      this.form1.num_sumli = this.form.num_sumli;
      this.socket.send(JSON.stringify(dataFinal))
      this.socket.onmessage = (event) => {
        const data = JSON.parse(event.data)
        console.log(data.type)
        if (data.type == "progress") {
          this.zantingList = [...this.zantingList, data.data];
        } else {
          this.zantingList = [...this.zantingList, data];
        }

        this.dataFinal1.jsId = this.$route.query.id;
        if (this.currentImage != null && this.currentImage != "") {
          const reusltData = {
            ...dataFinal,
            "resultStr": this.resultStr,
          }
          this.dataFinal1.jsResult = JSON.stringify(reusltData);
        } else {
          const reusltData = {
            ...dataFinal,
            "result": this.result,
          }
          this.dataFinal1.jsResult = JSON.stringify(reusltData);
        }
        this.dataFinal1.allImg = this.currentImage;
      }


    },
    testOld() {
      this.form.Hel_D = 12000;
      this.form.Hel_B = 300;
      this.form.Hel_v = 100;
      this.form.Hel_h = 300;
      this.form.Err_theta = 0.5;
      this.form.Err_D = 50;
      this.form.KT_x0 = 0;
      this.form.KT_y0 = 0;
      this.form.KT_v0 = 20;
      this.form.KT_H0 = 90;
      this.form.KT_DT_missle = 6000;
      this.form.KT_AT_hel = 3000;
      this.form.checkedHS = true;
      this.form.checkedHX = true;
      this.form.Jd_Sd = 45;
      this.form.V_missle = 0.85;
      this.form.Mis_hc = 17;
      this.form.Mis_D_Lamda = 16;
      this.form.Mis_D_Lamda_err = 1;
      this.form.Tao = 0.000002;
      this.form.Mis_MZD = "当前点";
      this.form.Time_fanying = 30;
      this.form.Mis_D_bc = 8;
      this.form.Sea_hk = 1;
      this.form.Rain_jiangyu = 0;
      this.form.delta_t = 0.3;
      this.form.num_sumli = 1000;
    },
    test() {
      this.form.Hel_D = 15000;
      this.form.Hel_B = 300;
      this.form.Hel_v = 100;
      this.form.Hel_h = 300;
      this.form.Err_theta = 0.1;
      this.form.Err_D = 30;
      this.form.KT_x0 = 0;
      this.form.KT_y0 = 0;
      this.form.KT_v0 = 20;
      this.form.KT_H0 = 90;
      this.form.KT_DT_missle = 7000;
      this.form.KT_AT_hel = 5000;
      this.form.checkedHS = true;
      this.form.checkedHX = true;
      this.form.Jd_Sd = 45;
      this.form.V_missle = 0.85;
      this.form.Mis_hc = 15;
      this.form.Mis_D_Lamda = 18;
      this.form.Mis_D_Lamda_err = 1;
      this.form.Tao = 0.000002;
      this.form.Mis_MZD = "当前点";
      this.form.Time_fanying = 30;
      this.form.Mis_D_bc = 8;
      this.form.Sea_hk = 2;
      this.form.Rain_jiangyu = 1;
      this.form.delta_t = 0.3;
      this.form.num_sumli = 1000;
    },
    save() {
      this.$axios({
        url: "http://127.0.0.1:10035/save/JsResult",//请求的后台接口
        method: "post",//get请求方式
        data: this.dataFinal1,
        withCredentials: true, // 关键：允许发送 Cookie
        headers: {
          'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res)
      })
    },





  },
  mounted() {
    this.initChart();
  }
};
</script>

<style scoped>
.background-container {
  padding: 0px;
  width: 95%;
  height: 93%;
  /* background-image: none;
  background-color: #fff; */
  /* 设置为视口高度 */
  background-size: cover;
  background-position: center;
  overflow: hidden;
  /* 隐藏超出背景图的内容 */
  margin-left: 2.5vw;
  margin-top: 2vw;
}

.scrollable-content {
  width: 100%;
  height: 100%;
  overflow: auto;
  scrollbar-width: none;
  /* Firefox */
}

/deep/ .el-checkbox__inner {
  width: 0.8vw;
  height: 0.8vw;
}

.selected-option {
  text-align: left;
  font-size: 0.7vw;
  display: flex;
  align-items: center;
  white-space: nowrap;
  width: 3vw;
  height: 100%;
  line-height: 4vh;
  padding-left: 0.5vw;
}

.options {
  border: 2px #00daff solid;
  width: 3.7vw;
  list-style: none;
  text-align: center;
  padding: 0;
  position: absolute;
  left: 11.5vw;
  top: 74vh;
  color: #fff;
  border-radius: 0.5vw;
  z-index: 99;
  font-size: 0.8vw;
  background-image: url('@/assets/img/optionBack.png');
  background-repeat: no-repeat;
  background-size: cover;
}

/deep/ .el-checkbox__inner::after {
  border: 0.2vw solid #fff;
  border-left: 0;
  border-top: 0;
  width: 25%;
  /* 调整勾选标记的宽度 */
  height: 80%;
  left: 30%;
  top: 5%;
}

.content-container {
  padding-left: 1vw;
  width: 100%;
  height: 100%;

  /* overflow-y: auto; */
  /* 添加垂直滚动条 */
}

/deep/ .el-form-item__label {
  color: #fff;
  width: 4vw;
  text-align: left;
  font-size: 0.7vw;
  line-height: 4vh;
  height: 100%;
}

/deep/ .el-form-item input-with-unit {
  height: 0.5vw;
}

/deep/ .el-input__inner {
  text-align: center;
  padding: 0%;
  font-size: 0.9vw;
  border-radius: 0;
  height: 0.8vw;
  width: 75%;
  height: 100%;
  border: none;
  background-color: transparent;
  color: #fff;
}

/deep/ .el-input {
  width: 4vw;
  height: 100%;
  font-size: 0;
}

.formaction3 /deep/ .el-input {
  width: 3vw;
  height: 100%;
  font-size: 0;
  /* width: 80%; */
}

.formaction3 /deep/ .el-input__inner {
  text-align: center;
  padding: 0%;
  font-size: 0.9vw;
  border-radius: 0;
  width: 100%;
  height: 100%;
  border: none;
}

.buttonLeft .el-button {
  width: 11vw;
  height: 4vh;
  margin-left: 1vw;
  margin-bottom: 1vh;
  line-height: 0.6vh;
  display: block;
  border-radius: 0;
  margin-bottom: 2vh;
  font-size: 0.7vw;
  background-color: transparent;
  border: none;
  color: #fff;
}

.buttonRight .el-button {
  width: 11vw;
  height: 4vh;
  margin-left: 1vw;
  margin-bottom: 1vh;
  line-height: 0.6vh;
  display: block;
  border-radius: 0;
  margin-bottom: 2vh;
  font-size: 0.7vw;
  background-color: transparent;
  border: none;
  color: #fff;
}

.el-button /deep/ .el-button__inner {
  text-align: center;
  font-size: 0.7vw;
  border-radius: 0;
  color: #fff;
  border: none;
  background-color: transparent;
}

/deep/ .el-form-item__content {
  margin-left: 0%;
  width: 80%;
  height: 4vh;
  font-size: 0;
}

/deep/ .select {
  width: 5vw;
  color: #fff;
  text-align: left;

}

/deep/ .el-image__error,
.el-image__placeholder {
  background: none;
}

/deep/ .el-image__inner {
  vertical-align: middle;
}

/deep/ .el-image {
  overflow: visible;
}

.xuanzexiala /deep/ .el-image {
  width: 2vw;
  height: 50%;
  display: flex;
  padding-right: 0.2vw;
  justify-content: flex-end;
  align-items: center;
}

.text {
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  width: 9.5vw;
  height: 3vh;
  line-height: 3vh;
  align-items: center;
  text-align: center;
  margin-left: -0.5vw;
}

.text2 {
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  width: 9.5vw;
  height: 3vh;
  line-height: 3vh;
  align-items: center;
  text-align: center;
}

.text1 {
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  width: 8vw;
  height: 3vh;
  line-height: 3vh;
  align-items: center;
  text-align: center;
}

.text3 {
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  width: 7vw;
  height: 3vh;
  line-height: 3vh;
  align-items: center;
  text-align: center;
  margin-right: 1vw;
}

.input-with-unit {
  display: flex;
  align-items: center;
  white-space: nowrap;
  margin-left: 3.1vw;
  text-align: right;
  justify-content: space-between;
  height: 4vh;
  margin-bottom: 0;
}

.buttonLeft {
  background-image: url('@/assets/img/buttonLeft.png');
  background-repeat: no-repeat;
  background-size: contain;
}

.buttonRight {
  background-image: url('@/assets/img/buttonRight.png');
  background-repeat: no-repeat;
  background-size: contain;
}

.biankuang {
  background-image: url('@/assets/img/form.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  margin-bottom: 2vh;
}

/deep/ .yibiaopantupian {
  z-index: 1;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

/deep/ .yibiaowenzi {
  z-index: 99;
  position: absolute;
  top: 40%;
  left: 18%;
}

/deep/ .yibiaopan {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  height: 100%;
  width: 100%;
  position: relative;
}

.yuanju {
  background-image: url('@/assets/img/yuanju.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  color: #fff;
  font-size: 0.7vw;
  white-space: nowrap;
  text-align: center;
  width: 70%;
  height: 30%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.biankuang /deep/ .el-input__inner {
  font-size: 1.5vw;
  height: 100%;
  color: aqua;
  background-color: transparent;
  border: none;
  width: 100%;
}

.info1111 /deep/ .el-input__inner {
  font-size: 0.8vw;
  height: 100%;
  color: aqua;
  background-color: transparent;
  border: none;
  width: 100%;
}

.yibiaopan .el-input {
  height: 100%;
}

.yibiaopan /deep/ .el-input__inner {
  font-size: 1.25vw;
  height: 100%;
  color: aqua;
  background-color: transparent;
  border: none;
  width: 3vw;
  text-align: right;

}

.buju {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 5.8vw;
  /* height: 10.4vh; */
  height: 5.8vw;
  margin-top: 1.4vh;
  margin-left: 3vw;
}

.yyinput /deep/ .el-input__inner {
  font-size: 1vw;
}

.yibiaopan /deep/ .el-form-item {
  margin: 0;
  line-height: 1;
}

.biaotou {
  background-image: url('@/assets/img/jianbianlv.png');
  height: 3vh;
}

.biaotou1 {
  background-image: url('@/assets/img/jianbianlv.png');
}


.back4 img {
  border-radius: 1vw;
  height: 90%;
  object-fit: contain;

}

.back {
  background-image: url('@/assets/img/back.png');
  background-size: 100% 100%;
  background-repeat: no-repeat;
}

.back1 {
  background-image: url('@/assets/img/back1.png');
  background-size: 100% 100%;
  background-repeat: no-repeat;
}

.back2 {
  background-image: url('@/assets/img/back2.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
}

.back3 {
  background-image: url('@/assets/img/back3.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
}

.back4 {
  background-image: url('@/assets/img/back4.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  width: 28vw;
  height: 34vh;
  margin-bottom: 1vh;
}

.back5 {
  background-image: url('@/assets/img/back5.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
}

.xialakuang {
  background-image: url('@/assets/img/xialakuang.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  background-color: transparent;
  width: 5vw;
  height: 3vh;
  display: flex;
  align-items: center;
}

.formaction {
  height: 3vh;
  display: flex;
  width: 100%;
  margin-bottom: 0.5vh;
  white-space: nowrap;
}

.formaction1 {
  height: 3vh;
  display: flex;
  justify-content: space-between;
  width: 14.5vw;
  padding-left: 1vw;
  margin-bottom: 0.5vh;
}

.formaction2 {
  height: 3vh;
  display: flex;
  justify-content: space-between;
  width: 9.5vw;
  padding-left: 1vw;
  margin-bottom: 0.5vh;
}

.formaction3 {
  height: 3vh;
  display: flex;
  width: 100%;
  padding-left: 0.5vw;
  margin-bottom: 0.5vh;
}

.formaction4 {
  height: 3vh;
  display: flex;
  width: 100%;
  margin-bottom: 1vh;
  justify-content: center;
}

.formaction5 {
  height: 3vh;
  display: flex;
  width: 100%;
  margin-bottom: 1vh;
  justify-content: center;
}

.formaction-checkbox {
  height: 3vh;
  display: flex;
  width: 14.5vw;
  padding-left: 1vw;
  margin-bottom: 0.5vh;
}

.formaction .el-input {
  display: flex;
  align-items: center;
  height: 2vh;
}

.formaction1 .el-input {
  display: flex;
  align-items: center;
  height: 100%;
}

.formaction /deep/ .el-input__inner {
  width: 100%;
  text-align: center;
}

.formaction1 /deep/ .el-input__inner {
  width: 100%;
  text-align: center;
}

ul :deep(li:hover) {
  background-color: #00fffc46 !important;
  border-radius: 0.5vw;
}

.xuanzexiala /deep/ .el-image__inner {
  width: 30%;
  height: 70%;
}

ul li {
  height: 3vh;
  line-height: 3vh;
}

.button1 {
  border-radius: 2vw;
  line-height: 0vh;
  background-image: url('@/assets/img/baocun.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  margin-left: 1vw;
}

.image2 /deep/ .el-image__inner {
  height: 60%;
  width: auto;
  height: 100%;
  font-size: 0;
  display: flex;
  align-items: center;
}

.biaotouqian /deep/ .el-image__inner {
  height: 15%;
  width: 100%;
}

.inputDiv {
  align-items: center;
  display: flex;
}

.inputDiv .el-input {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.xuanzexiala {
  /* background-image: url('@/assets/img/xialakuang.png');
  background-size: 100% 100%; */
  /* 拉伸图像以填充整个元素 */
  /* background-repeat: no-repeat;
  background-color: transparent; */
  width: 5vw;
  height: 3vh;
  display: flex;
  align-items: center;
}

/* .xuanzexiala .el-image {
  width: 1vw;
  height: 100%;
} */

/* .xuanzexiala .el-image__inner {
  width: 100%;
  height: 60%;
} */

.textArea .el-textarea {
  height: 24.5vh;
  font-size: 0.8vw;
}

.textArea /deep/ .el-textarea__inner {
  height: 100%;
  border: none;
  color: #fff;
  background-color: transparent;
}

.el-input--small .el-input__inner {
  width: 4vw !important;
}

/deep/ .el-icon-arrow-down,
/deep/ .el-icon-arrow-up {
  line-height: 0.8vh;
}

.formaction4 .el-button {
  width: 12vw;
  height: 3vh;
  line-height: 3vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.8vw;
  padding: 0;
}

.formaction5 .el-button {
  width: 5.8vw;
  height: 3vh;
  line-height: 3vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.8vw;
  padding: 0;
}

/deep/ .el-checkbox__label {
  font-size: 0.8vw;
  line-height: 0.8vw;
  padding-left: 0vw;
  color: #fff;
}

/deep/ .el-checkbox__input {
  line-height: 0.8vw;
}

.el-checkbox {
  border-radius: 50%;
  margin-right: 0.5vw;
  display: flex;
  align-items: center;
  justify-content: center;
}

.el-button + .el-button {
  margin-left: 0.5vw;
}

.waibiankuang {
  background-image: url('@/assets/img/wbk.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  padding-top: 2vh;
  padding-left: 1vw;
}


#missileChart {
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  position: absolute;
  z-index: 100000;
  background-color: #FFFFFF;
}
</style>
