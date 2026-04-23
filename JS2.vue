<template>
  <div style="width: 100%;height: 100%;">
    <div class="welcome" v-if="showWelcome">
      <img style="width: 100%;height: 100%;position: absolute;z-index:-1;" src="@/assets/img/loginBg.png">
      <div style="font-size: 3vw;color: #fff;width: 60vw;text-align: center;margin-left: 18%;padding-top: 22%;">
        欢迎使用自导作用距离计算软件
      </div>
    </div>
    <div class="background-container" v-if="showJS2">
      <div class="content-container">
        <div
          style="display: flex;width: 96%;margin-left: 17vw;margin-bottom: 1.5vh;margin-top: 4%;align-items: center;justify-items: center;justify-content: center;">
          <div style="display: flex;">
            <img src="http://127.0.0.1:10035/profile/xiaohui.png"
              style="width: 2.6%;position: absolute;object-fit: contain;left: 40%;">
            <div style="color: #fff; font-size: 1.6vw;font-weight: 500;">
            自导作用距离计算
          </div>
          </div>
          <el-button type="primary" class="button1" style="height: 1.5vw;margin-left: 30vw;"
            @click="save">保存</el-button>
        </div>
        <div style="display: flex;width: 76%;height: 70%;margin-left: 13%;" class="waibiankuang">
          <div style="display: flex;">
            <div style="display: flex;flex-direction: column;width: 12vw;margin-right: 1.5vw">
              <div style="display: flex;flex-direction: column;height: 30vh;margin-left: 0.5vw;margin-bottom: 2vh;"
                class="back">
                <div
                  style="display: flex;justify-content: space-between;width: 9.5vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                  class="biaotou">
                  <div style="vertical-align: middle;align-items: center;display: flex;">
                    <div style="display: flex;align-items: baseline;height: 100%;margin-left: 25%;" class="biaotouqian">
                      <el-image :src="require('@/assets/img/qianbiao.png')"
                        style="width: 0.6vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                    </div>
                    <div
                      style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;text-align: center;width: 100%;height: 100%;display: flex;">
                      直升机</div>
                  </div>
                </div>
                <div>
                  <div class="formaction">
                    <div class="text">航速/m/s</div>
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
                    <div class="text">距离/km</div>
                    <div class="inputDiv">
                      <el-input v-model="form.Hel_D" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                  <div class="formaction">
                    <div class="text">目标角度误差/°</div>
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
                  style="display: flex;justify-content: space-between;width: 9.5vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                  class="biaotou">
                  <div style="vertical-align: middle;align-items: center;display: flex;">
                    <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                      <el-image :src="require('@/assets/img/qianbiao.png')"
                        style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                    </div>
                    <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">导弹弹道</div>
                  </div>
                </div>
                <div>
                  <div class="xuanzhongbeijing" tabindex="0">
                    <div class="formaction">
                      <div class="text">相对方位/°</div>
                      <div class="inputDiv">
                        <el-input v-model="form.fangwei" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                      </div>
                    </div>
                  </div>
                  <div class="xuanzhongbeijing" tabindex="0">
                    <div class="formaction">
                      <div class="text">相对距离/m</div>
                      <div class="inputDiv">
                        <el-input v-model="form.juli" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
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
                      <div class="text">最大航程/Km</div>
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
                  style="display: flex;justify-content: space-between;width: 9.5vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                  class="biaotou">
                  <div style="vertical-align: middle;align-items: center;display: flex;">
                    <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                      <el-image :src="require('@/assets/img/qianbiao.png')"
                        style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                    </div>
                    <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">火控参数</div>
                  </div>
                </div>
                <div>
                  <div class="xuanzhongbeijing" tabindex="0">
                    <div class="formaction3">
                      <div class="text3">射击点选择</div>
                      <div style="width: 4vw;text-align: left;color: #fff;height: 2.5vh;" @click="showOptions"
                        @focus="onFocus1" @blur="onBlur1" tabindex="0">
                        <div class="xuanzexiala" style="display: flex;width: 100%;height: 100%;position: relative;">
                          <div class="selected-option">
                            {{ this.form.Mis_MZD || '' }}
                          </div>
                          <el-image :src="require('@/assets/img/xialajiantou.png')"
                            style="display: flex;align-items: center;"></el-image>
                        </div>
                      </div>
                      <ul v-if="showOptions2" class="options">
                        <li v-for="(option, index) in mzdList" :key="index" @click="selectOption2(option)">
                          {{ option.label }}
                        </li>
                      </ul>
                    </div>
                  </div>
                  <div class="formaction3">
                    <div class="text3">反应时间/s</div>
                    <div class="inputDiv">
                      <el-input v-model="form.Time_fanying" autocomplete="off" @focus="onFocus"
                        @blur="onBlur"></el-input>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div style="display: flex;flex-direction: column;width: 31vw;">
              <div style="display: flex;margin-bottom: 2vh">
                <div class="back1"
                  style="height: 30vh;display: flex;flex-direction: column;width: 14vw;margin-right: 1.5vw;">
                  <div
                    style="display: flex;justify-content: space-between;width: 12vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                    class="biaotou">
                    <div style="vertical-align: middle;align-items: center;display: flex;">
                      <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                        <el-image :src="require('@/assets/img/qianbiao.png')"
                          style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                      </div>
                      <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">快艇</div>
                    </div>
                  </div>
                  <div style="display: flex;flex-direction: column;justify-content:space-between;">
                    <div class="xuanzhongbeijing" tabindex="0">
                      <div class="formaction">
                        <div class="text2">初始x位置/m</div>
                        <div class="inputDiv">
                          <el-input v-model="form.KT_x0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">初始y位置/m</div>
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
                      <div class="text2">初始航速/kn</div>
                      <div class="inputDiv">
                        <el-input v-model="form.KT_v0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">导弹探测距离/km</div>
                      <div class="inputDiv">
                        <el-input v-model="form.KT_DT_missle" autocomplete="off" @focus="onFocus"
                          @blur="onBlur"></el-input>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">对空攻击距离/km</div>
                      <div class="inputDiv">
                        <el-input v-model="form.KT_AT_hel" autocomplete="off" @focus="onFocus"
                          @blur="onBlur"></el-input>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text1" style="width: 7vw;">机动/km</div>
                      <div style="display: flex;align-items: center;justify-content: center;">
                        <el-checkbox v-model="checked">航向</el-checkbox>
                        <el-checkbox v-model="checked">航速</el-checkbox>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="back1"
                  style="height: 30vh;display: flex;flex-direction: column;width: 14vw;margin-right: 1.5vw;">
                  <div
                    style="display: flex;justify-content: space-between;width: 12vw;margin-bottom: 2vh;margin-top: 1vh;margin-left: 1vw;"
                    class="biaotou">
                    <div style="vertical-align: middle;align-items: center;display: flex;">
                      <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                        <el-image :src="require('@/assets/img/qianbiao.png')"
                          style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                      </div>
                      <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">仿真控制</div>
                    </div>
                  </div>
                  <div style="display: flex;flex-direction: column;justify-content:space-between;">
                    <div class="xuanzhongbeijing" tabindex="0">
                      <div class="formaction">
                        <div class="text2">仿真步长/m</div>
                        <div class="inputDiv">
                          <el-input v-model="form.delta_t" autocomplete="off" @focus="onFocus"
                            @blur="onBlur"></el-input>
                        </div>
                      </div>
                    </div>
                    <div class="formaction">
                      <div class="text2">仿真次数</div>
                      <div class="inputDiv">
                        <el-input v-model="form.num_sumli" autocomplete="off" @focus="onFocus"
                          @blur="onBlur"></el-input>
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
                      <el-button class="button3">暂停</el-button>
                    </div>
                    <div class="formaction5">
                      <el-button class="button3">结束计算</el-button>
                      <el-button class="button3">清除图片</el-button>
                    </div>
                  </div>
                </div>
              </div>
              <div style="display: flex;margin-bottom: 2vh;">
                <div style="display: flex;margin-bottom: 2vh;flex-direction: column;width: 14vw;margin-right: 1.5vw;">
                  <div style="display: flex;flex-direction: column;height: 20vh;margin-bottom: 2vh;" class="back1">
                    <div
                      style="display: flex;justify-content: space-between;width: 12vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                      class="biaotou">
                      <div style="vertical-align: middle;align-items: center;display: flex;">
                        <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                          <el-image :src="require('@/assets/img/qianbiao.png')"
                            style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
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
                        <div class="text2">脉冲宽度/us</div>
                        <div class="inputDiv">
                          <el-input v-model="form.Tao" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div style="display: flex;flex-direction: column;height: 13.5vh;margin-bottom: 1vh;" class="back1">
                    <div
                      style="display: flex;justify-content: space-between;width: 12vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                      class="biaotou">
                      <div style="vertical-align: middle;align-items: center;display: flex;">
                        <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                          <el-image :src="require('@/assets/img/qianbiao.png')"
                            style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                        </div>
                        <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">环境参数</div>
                      </div>
                    </div>
                    <div>
                      <div class="xuanzhongbeijing" tabindex="0">
                        <div class="formaction3">
                          <div class="text2">海况等级</div>
                          <div class="inputDiv">
                            <el-input v-model="form.Sea_hk" autocomplete="off" @focus="onFocus"
                              @blur="onBlur"></el-input>
                          </div>
                        </div>
                      </div>
                      <div class="formaction3">
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
                      style="display: flex;justify-content: space-between;width: 12vw;margin-bottom: 2vh;margin-top: 1vh;margin-left: 1vw;"
                      class="biaotou">
                      <div style="vertical-align: middle;align-items: center;display: flex;">
                        <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                          <el-image :src="require('@/assets/img/qianbiao.png')"
                            style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                        </div>
                        <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">结果输出</div>
                      </div>
                    </div>
                    <div style="display: flex;flex-direction: column;justify-content:space-between;">
                      <div class="xuanzhongbeijing" tabindex="0">
                        <div class="formaction">
                          <div class="text2">导弹航程/m</div>
                          <div class="inputDiv">
                            <el-input v-model="form.Mis_sc" autocomplete="off" @focus="onFocus"
                              @blur="onBlur"></el-input>
                          </div>
                        </div>
                      </div>
                      <div class="formaction">
                        <div class="text2">导弹高度/m</div>
                        <div class="inputDiv">
                          <el-input v-model="form.Mis_gd" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction">
                        <div class="text2">击水概率</div>
                        <div class="inputDiv">
                          <el-input v-model="form.jiShuiResult" autocomplete="off" @focus="onFocus"
                            @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction">
                        <div class="text2">波门上限/m</div>
                        <div class="inputDiv">
                          <el-input v-model="form.Mis_Serch_up" autocomplete="off" @focus="onFocus"
                            @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction">
                        <div class="text2">波门下限/m</div>
                        <div class="inputDiv">
                          <el-input v-model="form.Mis_Serch_down" autocomplete="off" @focus="onFocus"
                            @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction4" style="margin-top: 1vh;">
                        <div class="inputDiv">
                          <el-button>评估</el-button>
                        </div>
                      </div>
                      <div class="formaction">
                        <div class="text2">命中概率</div>
                        <div class="inputDiv">
                          <el-input v-model="result" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
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
                  <img :src="currentImage" style="height: 100%;justify-items: center;" />
                </div>
              </div>
              <div class="back4" style="display: flex;flex-direction: column;height: 32.5vh;">
                <div
                  style="display: flex;justify-content: space-between;width: 28vw;margin-bottom: 1.5vh;margin-top: 1vh;margin-left: 1vw;"
                  class="biaotou">
                  <div style="vertical-align: middle;align-items: center;display: flex;">
                    <div style="display: flex;align-items: baseline;height: 100%;margin-left: 25%;" class="biaotouqian">
                      <el-image :src="require('@/assets/img/qianbiao.png')"
                        style="width: 0.6vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                    </div>
                    <div
                      style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;text-align: center;width: 100%;height: 100%;display: flex;">
                      消息呈现栏</div>
                  </div>
                </div>
                <div class="textArea">
                  <el-input type="textarea" :rows="2" v-model="resultStr">
                  </el-input>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentImage: null,
      socket: null,
      showWelcome: true,
      showJS2: false,
      dataFinal1: {
        jsId: null,
        jsResult: {},
        allImg: null,
      },
      showOptions2: false,
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
        Mis_hc: 0,
        Mis_MZD: 0,
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
      }
    };
  },
  beforeDestroy() {
    if (this.socket) {
      this.socket.close();
    }
  },
  created() {
    // 连接 FastAPI WebSocket
    this.socket = new WebSocket('ws://127.0.0.1:9086/ws');
    console.log(this.socket)

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
    clearImage() {
      this.src = "";
    },
    dataInitialize() {
      this.form = {
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
        V_missle: 0,
        Mis_hc: 0,
        Mis_sc: 0,
        Mis_D_Lamda: 0,
        Mis_D_Lamda_err: 0,
        Mis_D_bc: 0,
        Sea_hk: 0,
        MM: 0,
        delta_t: 0,
        num_sumli: 0,
      }
    },
    onFocus(event) {
      const parentDiv = event.target.closest('.formaction');
      console.log(parentDiv)
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
      console.log(parentDiv);
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
      console.log(option)
      this.form.Mis_MZD = option.value;
      console.log(this.form.Mis_MZD)
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
        "num_sumli": this.form.num_sumli
      };
      if (dataFinal.Mis_MZD == "当前点") {
        dataFinal.Mis_MZD = 0;
      } else {
        dataFinal.Mis_MZD = 1;
      }
      this.connectWebSocket(dataFinal)

    },
    connectWebSocket(dataFinal) {
      // 创建WebSocket连接
      // dataFinal = {
      //   // 直升机参数
      //   "Hel_D": 10,
      //   "Hel_B": 10,
      //   "Hel_v": 10,
      //   "Hel_h": 10,

      //   // 误差参数
      //   "Err_theta": 10,
      //   "Err_D": 10,

      //   // 快艇参数
      //   "KT_x0": 10,
      //   "KT_y0": 10,
      //   "KT_v0": 10,
      //   "KT_H0": 10,
      //   "KT_DT_missle": 10,
      //   "KT_AT_hel": 10,

      //   // 导弹参数
      //   "V_missle": 10,
      //   "Mis_hc": 10,
      //   "Mis_sc": 10,
      //   "Mis_D_Lamda": 10,
      //   "Mis_D_Lamda_err": 10,
      //   "Mis_D_bc": 10,

      //   // 环境参数
      //   "Sea_hk": 10,

      //   // 其他参数
      //   "MM": 10,
      //   "delta_t": 10,
      //   "num_sumli": 10,
      // };
      // console.log(dataFinal)
      // this.socket.send("123")
      this.socket.send(JSON.stringify(dataFinal))
      this.socket.onmessage = (event) => {
        const data = JSON.parse(event.data)
        console.log(data)
        if (data.type === 'chart_update') {
          this.currentImage = data.image
          this.resultStr = data.result
          // this.updateCount = data.count
        }
        if (data.type === 'result_update') {
          this.resultStr = data.result
          this.form.Mis_sc = data.Mis_sc
          this.form.Mis_gd = data.Mis_gd
          this.form.jiShuiResult = data.jiShuiResult
          this.form.Mis_Serch_up = data.Mis_Serch_up
          this.form.Mis_Serch_down = data.Mis_Serch_down
          // this.updateCount = data.count
        }
        if (data.type === 'average_update') {
          this.result = data.str
          console.log(this.result)
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

      // this.socket.onclose = () => {
      //   console.log('WebSocket连接关闭')
      // }
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
      this.form.V_missle = 0.8;
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
    }
  },
  mounted(){
    setTimeout(() => {
      this.showWelcome = false;
      this.showJS2 = true;
    }, 3000);
  }
};
</script>

<style scoped>
.background-container {
  padding: 0px;
  width: 100%;
  height: 100%;
  background-image: url('~@/assets/img/copybg.png');
  /* background-image: none;
  background-color: #fff; */
  /* 设置为视口高度 */
  background-size: cover;
  background-position: center;
  overflow: hidden;
  /* 隐藏超出背景图的内容 */
}

.scrollable-content {
  width: 100%;
  height: 100%;
  overflow: auto;
  scrollbar-width: none;
  /* Firefox */
}

/deep/.el-checkbox__inner {
  width: 0.8vw;
  height: 0.8vw;
  border-radius: 50%;
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
  width: 3.5vw;
  list-style: none;
  text-align: center;
  padding: 0;
  position: absolute;
  left: 11.8vw;
  top: 73vh;
  color: #fff;
  border-radius: 0.5vw;
  z-index: 99;
  font-size: 0.8vw;
  background-image: url('@/assets/img/optionBack.png');
  background-repeat: no-repeat;
  background-size: cover;
}

/deep/.el-checkbox__inner::after {
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

/deep/.el-form-item input-with-unit {
  height: 0.5vw;
}

/deep/.el-input__inner {
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

/deep/.el-input {
  width: 4vw;
  height: 100%;
  font-size: 0;
  /* width: 80%; */
}

.formaction3 /deep/.el-input {
  width: 4vw;
  height: 100%;
  font-size: 0;
  /* width: 80%; */
}

.formaction3 /deep/.el-input__inner {
  text-align: center;
  padding: 0%;
  font-size: 0.9vw;
  border-radius: 0;
  width: 100%;
  height: 100%;
  border: none;
  padding-right: 1vw;
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

.el-button /deep/.el-button__inner {
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
  width: 7.5vw;
  height: 3vh;
  line-height: 3vh;
  align-items: center;
  text-align: center;
  margin-left: 0.5vw;
}

.text2 {
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  width: 10.5vw;
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
  width: 6vw;
  height: 3vh;
  line-height: 3vh;
  align-items: center;
  text-align: center;
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
  width: 30vw;
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

.xuanzexiala {
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

.textArea /deep/.el-textarea__inner {
  height: 100%;
  border: none;
  color: #fff;
  background-color: transparent;
}

.el-input--small .el-input__inner {
  width: 4vw !important;
}

/deep/.el-icon-arrow-down,
/deep/.el-icon-arrow-up {
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

/deep/.el-checkbox__label {
  font-size: 0.8vw;
  line-height: 0.8vw;
  padding-left: 0vw;
  color: #fff;
}

/deep/.el-checkbox__input {
  line-height: 0.8vw;
}

.el-checkbox {
  border-radius: 50%;
  margin-right: 0.5vw;
  display: flex;
  align-items: center;
  justify-content: center;
}

.el-button+.el-button {
  margin-left: 0.5vw;
}

.waibiankuang {
  background-image: url('@/assets/img/wbk.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  padding-top: 2vh;
  padding-left: 1vw;
}
</style>
