<template>
  <div class="background-container">
    <div class="content-container">
      <div
        style="display: flex;width: 96%;margin-left: 12vw;margin-bottom: 1.5vh;margin-top: 1.5vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color: #fff; font-size: 1.6vw;font-weight: 500;">
          舰载直升机航空鱼雷作战使用辅助决策软件
        </div>
        <el-button type="primary" class="button1" style="height: 1.5vw;margin-left: 30vw;" @click="save">保存</el-button>
      </div>
      <div style="display: flex;width: 92.5%;height: 87%;" class="waibiankuang">
        <div style="display: flex;">
          <div style="display: flex;flex-direction: column;width: 15vw;margin-right: 1.5vw">
            <div style="display: flex;flex-direction: column;height: 37vh;margin-left: 0.5vw;margin-bottom: 1vh;"
              class="back">
              <div
                style="display: flex;justify-content: space-between;width: 13vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                class="biaotou">
                <div style="vertical-align: middle;align-items: center;display: flex;">
                  <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                    <el-image :src="require('@/assets/img/qianbiao.png')"
                      style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                  </div>
                  <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">直升机</div>
                </div>
              </div>
              <div>
                <div class="xuanzhongbeijing" tabindex="0">
                  <div class="formaction">
                    <div class="text">航向/°</div>
                    <div class="inputbg">
                      <el-input v-model="form.h_c0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">航速/m/s</div>
                  <div class="inputbg">
                    <el-input v-model="form.h_v" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">高度/m</div>
                  <div class="inputbg">
                    <el-input v-model="form.h_h" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">投雷方位/°</div>
                  <div class="inputbg">
                    <el-input v-model="form.yl_b" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">投雷距离/m</div>
                  <div class="inputbg">
                    <el-input v-model="form.yl_d" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">投雷延时/min</div>
                  <div class="inputbg">
                    <el-input v-model="form.t_zb" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
<!--                <div class="formaction">-->
<!--                  <div class="text">目标角度误差/°</div>-->
<!--                  <div class="inputDiv">-->
<!--                    <el-input v-model="form.Err_theta" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>-->
<!--                  </div>-->
<!--                </div>-->
<!--                <div class="formaction">-->
<!--                  <div class="text">目指距离误差/m</div>-->
<!--                  <div class="inputDiv">-->
<!--                    <el-input v-model="form.Err_D" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>-->
<!--                  </div>-->
<!--                </div>-->
                <div class="formaction">
                  <div class="text">目指角度误差/°</div>
                  <div class="inputbg">
                    <el-input v-model="form.err_dx" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">目指距离误差/m</div>
                  <div class="inputbg">
                    <el-input v-model="form.err_dy" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
              </div>
            </div>
            <div class="back1" style="height: 30.5vh;margin-left: 0.5vw;display: flex;flex-direction: column;">
              <div
                style="display: flex;justify-content: space-between;width: 13vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                class="biaotou">
                <div style="vertical-align: middle;align-items: center;display: flex;">
                  <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                    <el-image :src="require('@/assets/img/qianbiao.png')"
                      style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                  </div>
                  <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">潜艇</div>
                </div>
              </div>
              <div style="display: flex;flex-direction: column;justify-content:space-between;">
                <div class="xuanzhongbeijing" tabindex="0">
                  <div class="formaction">
                    <div class="text">初始x位置/m</div>
                    <div class="inputbg">
                      <el-input v-model="form.qt_x00" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">初始y位置/m</div>
                  <div class="inputbg">
                    <el-input v-model="form.qt_y00" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">航速/kn</div>
                  <div class="inputbg">
                    <el-input v-model="form.qt_v0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">初始航向/°</div>
                  <div class="inputbg">
                    <el-input v-model="form.qt_h0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">反射强度/dB</div>
                  <div class="inputbg">
                    <el-input v-model="form.ts0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction">
                  <div class="text">报警距离/m</div>
                  <div class="inputbg">
                    <el-input v-model="form.ylbg_jl" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div style="display: flex;flex-direction: column;width: 57vw; margin-left: -1vw">
            <div style="display: flex;margin-bottom: 2vh">
              <div style="display: flex;flex-direction: column;width: 32vw;height: 37vh;margin-right: 1.5vw;"
                class="back2">
                <div
                  style="display: flex;justify-content: space-between;width: 29.5vw;margin-bottom: 2vh;margin-left: 1vw;margin-top: 1vh;"
                  class="biaotou">
                  <div style="vertical-align: middle;align-items: center;display: flex;">
                    <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                      <el-image :src="require('@/assets/img/qianbiao.png')"
                        style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                    </div>
                    <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">鱼雷</div>
                  </div>
                </div>
                <div style="display: flex; flex-direction: row;width: 100%; justify-content: space-between">
                  <div class="back1"
                    style="height: 29vh;margin-left: 0.6vw; margin-right: 0.2vw; display: flex;flex-direction: column; width: 15vw">
                    <div
                      style="display: flex;justify-content: space-between;width: 13.5vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                      class="biaotou">
                      <div style="vertical-align: middle;align-items: center;display: flex;">
                        <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                          <el-image :src="require('@/assets/img/qianbiao.png')"
                            style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                        </div>
                        <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">弹道参数</div>
                      </div>
                    </div>
                    <div style="display: flex;flex-direction: column;justify-content:space-between;">
                      <div class="xuanzhongbeijing" tabindex="0">
                        <div class="formaction1">
                          <div class="text">航程/m</div>
                          <div class="inputbg">
                            <el-input v-model="form.yl_hc" autocomplete="off" @focus="onFocus"
                              @blur="onBlur"></el-input>
                          </div>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">航速/kn</div>
                        <div class="inputbg">
                          <el-input v-model="form.v_yl" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">工作深度/m</div>
                        <div class="inputbg">
                          <el-input v-model="form.h_yl" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">无动力时间/s</div>
                        <div class="inputbg">
                          <el-input v-model="form.t_wdl" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">旋回半径/m</div>
                        <div class="inputbg">
                          <el-input v-model="form.r_t" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">角度变化率/°/s</div>
                        <div class="inputbg">
                          <el-input v-model="form.omiga_detle" autocomplete="off" @focus="onFocus"
                            @blur="onBlur"></el-input>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="back1"
                    style="height: 29vh; margin-left: 0.2vw; margin-right: 0.6vw;display: flex;flex-direction: column; width: 15vw">
                    <div
                      style="display: flex;justify-content: space-between;width: 13.5vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                      class="biaotou">
                      <div style="vertical-align: middle;align-items: center;display: flex;">
                        <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                          <el-image :src="require('@/assets/img/qianbiao.png')"
                            style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                        </div>
                        <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">自导参数</div>
                      </div>
                    </div>
                    <div style="display: flex;flex-direction: column;justify-content:space-between;">
                      <div class="xuanzhongbeijing" tabindex="0">
                        <div class="formaction1">
                          <div class="text">扇面半开角/°</div>
                          <div class="inputbg">
                            <el-input v-model="form.lamda" autocomplete="off" @focus="onFocus"
                              @blur="onBlur"></el-input>
                          </div>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">声源级/dB</div>
                        <div class="inputbg">
                          <el-input v-model="form.sl" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">频率/kHZ</div>
                        <div class="inputbg">
                          <el-input v-model="form.f" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">接收指向性指数/dB</div>
                        <div class="inputbg">
                          <el-input v-model="form.di" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">检测阈值/dB</div>
                        <div class="inputbg">
                          <el-input v-model="form.dt" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                      <div class="formaction1">
                        <div class="text">毁伤范围/m</div>
                        <div class="inputbg">
                          <el-input v-model="form.yl_yinxin" autocomplete="off" @focus="onFocus"
                            @blur="onBlur"></el-input>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="back4" style="margin-left: -1vw">
                <div style="height: 96%;width: 100%;margin-top: 1%;display: flex;justify-content: center;">
                  <img :src="currentImage" @click="showBigInfo()" style="height: 100%;justify-items: center;" />
                </div>

              </div>
            </div>
            <div style="display: flex; margin-top: -1vh;">
              <div
                style="width: 20vw;margin-right: 1.5vw;border-radius: 1vw;display: flex;height: 30.4vh;flex-direction: column;"
                class="back3">
                <div
                  style="display: flex;justify-content: space-between;width: 18vw;margin-bottom: 2vh;margin-left: 1vw;margin-top: 1vh;"
                  class="biaotou">
                  <div style="vertical-align: middle;align-items: center;display: flex;">
                    <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                      <el-image :src="require('@/assets/img/qianbiao.png')"
                        style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                    </div>
                    <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">潜艇对抗措施</div>
                  </div>
                </div>
                <div style="display: flex;flex-direction: column; margin-top: -1.4vh">
                  <div class="back1"
                    style="height: 9vh;margin-left: 0.6vw; margin-right: 0.2vw; display: flex;flex-direction: column; width: 18.8vw">
                    <div
                      style="display: flex;justify-content: space-between;width: 17.5vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                      class="biaotou">
                      <div style="vertical-align: middle;align-items: center;display: flex;">
                        <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                          <el-image :src="require('@/assets/img/qianbiao.png')"
                            style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                        </div>
                        <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">机动</div>
                      </div>
                    </div>
                    <div style="display: flex; width: 18.2vw; flex-direction: row; margin-top: -1vh">
                      <div class="formaction-checkbox">
                        <input type="checkbox" id="option1" name="jidongradio" v-model="form.flag_jidong">
                        <label for="option1">是</label>
                      </div>
                      <div class="formaction1">
                        <div class="text">机动速度/kn&nbsp;</div>
                        <div class="inputbg">
                          <el-input v-model="form.qt_xh" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="back1"
                    style="height: 15vh;margin-top: 0.5vh;margin-left: 0.6vw; margin-right: 0.2vw; display: flex;flex-direction: column; width: 18.8vw">
                    <div
                      style="display: flex;justify-content: space-between;width: 17.5vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                      class="biaotou">
                      <div style="vertical-align: middle;align-items: center;display: flex;">
                        <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                          <el-image :src="require('@/assets/img/qianbiao.png')"
                            style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                        </div>
                        <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">悬浮式噪声干扰器</div>
                      </div>
                    </div>
                    <div style="display: flex; flex-direction: row; margin-top: -1vh">
                      <div style="display: flex; flex-direction: column">
                        <div class="formaction-checkbox" style="width: 5vw;">
                          <input type="checkbox" id="option1" name="jidongradio" v-model="form.flag_ganraoqi">
                          <label for="option1">释放</label>
                        </div>
                        <div class="formaction2" style="width: 5vw;display: flex;">
                          <div class="text">距离/m</div>
                          <div class="inputbg">
                            <el-input v-model="form.gr_d" autocomplete="off" @focus="onFocus" @blur="onBlur"
                              style="width: 3vw;"></el-input>
                          </div>
                        </div>
                        <div class="formaction2"
                          style="width: 5vw;display: flex;">
                          <div class="text" style="margin-right: 0.5vw;">舷角/°</div>
                          <div class="inputbg">
                            <el-input v-model="form.gr_q" autocomplete="off" @focus="onFocus" @blur="onBlur"
                              style="width: 3vw;"></el-input>
                          </div>
                        </div>
                      </div>
                      <div style="display: flex; flex-direction: column;">
                        <div class="formaction2" style="width: 11vw;">
                          <div class="text" style="margin-right: 1.4vw;">&nbsp;辐射噪声级/dB</div>
                          <div class="inputbg">
                            <el-input v-model="form.sl_gr" autocomplete="off" @focus="onFocus"
                              @blur="onBlur" style="width: 3vw"></el-input>
                          </div>
                        </div>
                        <div class="formaction2" style="width: 11vw;">
                          <div class="text" style="margin-right: 0.1vw;">&nbsp;辐射噪声宽度/kHz</div>
                          <div class="inputbg">
                            <el-input v-model="form.df_gr" autocomplete="off" @focus="onFocus"
                              @blur="onBlur" style="width: 3vw"></el-input>
                          </div>
                        </div>
                        <div class="formaction2" style="width: 11vw;">
                          <div class="text">&nbsp;接收噪声宽度/kHz</div>
                          <div class="inputbg">
                            <el-input v-model="form.dfjs_gr" autocomplete="off" @focus="onFocus"
                              @blur="onBlur" style="width: 3vw"></el-input>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="back1"
                style="height: 30.4vh;margin-left: -1vw;display: flex;flex-direction: column;width: 14vw;">
                <div
                  style="display: flex;justify-content: space-between;width: 13vw;margin-bottom: 2vh;margin-left: 0.5vw;margin-right:0.5vw; margin-top: 1vh;"
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
                    <div class="formaction" style="width: 10.5vw;margin-bottom: 0.7vh;">
                      <div class="text">仿真步长/s</div>
                      <div class="inputbg">
                        <el-input v-model="form.delta_t" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                      </div>
                    </div>
                  </div>
                  <div class="formaction" style="width: 10.5vw;margin-bottom: 0.7vh;">
                    <div class="text">海况等级</div>
                    <div class="inputbg">
                      <el-input v-model="form.s_hk" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                  <div class="formaction" style="width: 10.5vw;margin-bottom: 0.7vh;">
                    <div class="text">海区深度</div>
                    <div class="inputbg">
                      <el-input v-model="form.hqsd" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                    </div>
                  </div>
                  <div class="formaction5">
                    <el-button class="button3" @click="test">载入测试值</el-button>
                    <el-button class="button3" @click="dataInitialize">数据初始化</el-button>
                  </div>
                  <div class="formaction5">
                    <el-button class="button3" @click="submitForm">计算</el-button>
                    <el-button class="button3" @click="finishComp">结束计算</el-button>
                  </div>
                  <div class="formaction5">
                    <el-button class="button3" @click="zanting = zanting === 1 ? 0 : 1">
                      {{ zanting === 1 ? '继续' : '暂停' }}</el-button>
                    <el-button class="button3" @click="clear">清除数据</el-button>
                  </div>
                </div>
              </div>
              <div
                style="height: 30.4vh;width: 29vw;border-radius: 1vw;display: flex;flex-wrap: wrap;flex-direction: column;">
                <div class="back1"
                  style="height: 9vh;margin-left: 0.6vw; margin-right: 0.2vw; display: flex;flex-direction: column; width: 22.3vw">
                  <div
                    style="display: flex;justify-content: space-between;width: 20.8vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                    class="biaotou">
                    <div style="vertical-align: middle;align-items: center;display: flex;">
                      <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                        <el-image :src="require('@/assets/img/qianbiao.png')"
                          style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                      </div>
                      <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">结果输出</div>
                    </div>
                  </div>
                  <div style="display: flex; flex-direction: row; margin-top: -1vh">
                    <div class="formaction1" style="width: 9.5vw;">
                      <div class="text" >鱼雷航程/m</div>
                      <div class="inputbg2">
                        <el-input v-model="form.finalHc" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  ></el-input>
                      </div>
                    </div>
                    <div class="formaction1" style="width: 9.5vw;">
                      <div class="text">声自导距离/m</div>
                      <div class="inputbg2">
                        <el-input v-model="form.finalZD" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  ></el-input>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="back1"
                  style="height: 9vh;margin-top: 0.5vh;margin-left: 0.6vw; margin-right: 0.2vw; display: flex;flex-direction: column; width: 22.3vw">
                  <div
                    style="display: flex;justify-content: space-between;width: 20.8vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                    class="biaotou">
                    <div style="vertical-align: middle;align-items: center;display: flex;">
                      <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                        <el-image :src="require('@/assets/img/qianbiao.png')"
                          style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                      </div>
                      <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">效能评估</div>
                    </div>
                  </div>
                  <div style="display: flex; flex-direction: row; margin-top: -1vh;">
                    <div style="display: flex;">
                      <div class="formaction2">
                        <div class="text">仿真次数</div>
                        <div class="inputbg2">
                        <el-input v-model="form.fz_num" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  ></el-input>
                      </div>
                      </div>
                    </div>
                    <div style="display: flex;">
                      <button
                        style="width: 2.5vw;height: 3vh;white-space: nowrap;font-size: 0.8vw;display: flex;justify-content: center;align-items: center;" @click="submitForm">评估</button>
                    </div>
                    <div style="display: flex; flex-direction: column">
                      <div class="formaction2" style="width: 7.8vw;">
                        <div class="text">命中概率</div>
                        <div class="inputbg2">
                        <el-input v-model="form.result" autocomplete="off" @focus="onFocus" @blur="onBlur"
                                  ></el-input>
                      </div>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="back1"
                  style="height: 11vh;margin-top: 0.5vh;margin-left: 0.6vw; margin-right: 0.2vw; display: flex;flex-direction: column; width: 22.3vw">
                  <div
                    style="display: flex;justify-content: space-between;width: 20.8vw;margin-bottom: 2vh;margin-left: 0.7vw;margin-top: 1vh;"
                    class="biaotou">
                    <div style="vertical-align: middle;align-items: center;display: flex;">
                      <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                        <el-image :src="require('@/assets/img/qianbiao.png')"
                          style="width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;display: inline-flex;align-items: center;" />
                      </div>
                      <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">消息呈现栏</div>
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
    </div>

    <el-dialog title="预览" :visible.sync="showBig">
      <div style="height: 20vw;width: 20vw;margin: 0 auto">
        <img :src="currentImage" style="height: 100%;object-fit: contain;">
      </div>

    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showBig:false,
      zanting:0,
      form1: null,
      zantingList:[],
      currentImage: '',
      socket: null,
      resultStr: "",
      dataFinal1: {
        jsId: null,
        jsResult: {},
        allImg: null,
      },
      form: {
        h_c0: 0,
        h_v: 0,
        h_h: 0,
        yl_b: 0,
        yl_d: 0,
        t_zb: 0,
        err_dx: 0,
        err_dy: 0,
        yl_hc: 0,
        v_yl: 0,
        h_yl: 0,
        t_wdl: 0,
        r_t: 0,
        omiga_detle: 0,
        lamda: 0,
        sl: 0,
        f: 0,
        di: 0,
        dt: 0,
        yl_yinxin: 0,
        qt_x00: 0,
        qt_y00: 0,
        qt_v0: 0,
        qt_h0: 0,
        ts0: 0,
        ylbg_jl: 0,
        qt_xh: 0,
        flag_jidong: 0,
        sl_gr: 0,
        gr_d: 0,
        dfjs_gr: 0,
        gr_q: 0,
        df_gr: 0,
        flag_ganraoqi: 0,
        delta_t: 0,
        s_hk: 0,
        fz_num: 0,
        result: 0,
        finalHc: 0,
        finalZD: 0,
        hqsd:0,
      }
    };
  },
  methods: {
    showBigInfo(){
      this.showBig = true;

    },
    clear() {
      this.currentImage = "";
      this.form.h_c0 = 0;
      this.form.h_v = 0;
      this.form.h_h = 0;
      this.form.yl_b = 0;
      this.form.yl_d = 0;
      this.form.t_zb = 0;
      this.form.err_dx = 0;
      this.form.err_dy = 0;
      // 鱼雷弹道参数
      this.form.yl_hc = 0;
      this.form.v_yl = 0;
      this.form.h_yl = 0;
      this.form.t_wdl = 0;
      this.form.r_t = 0;
      this.form.omiga_detle = 0;
      // 鱼雷自导参数
      this.form.lamda = 0;
      this.form.sl = 0;
      this.form.f = 0;
      this.form.di = 0;
      this.form.dt = 0;
      this.form.yl_yinxin = 0;
      // 潜艇参数
      this.form.qt_x00 = 0;
      this.form.qt_y00 = 0;
      this.form.qt_v0 = 0;
      this.form.qt_h0 = 0;
      this.form.ts0 = 0;
      this.form.ylbg_jl = 0;
      // 潜艇机动参数
      this.form.qt_xh = 0;
      this.form.flag_jidong = false;
      // 干扰器参数
      this.form.sl_gr = 0;
      this.form.gr_d = 0;
      this.form.dfjs_gr = 0;
      this.form.gr_q = 0;
      this.form.df_gr = 0;
      this.form.flag_ganraoqi = false;
      // 仿真控制
      this.form.delta_t = 0;
      this.form.s_hk = 0;
      this.form.fz_num = 0;
      this.form.hqsd = 0;
      //结果输出
      this.form.finalHc = 0;
      this.form.finalZD = 0;
      //效能评估
      this.form.fz_num = 0;
      this.form.result = 0;
      //消息呈现栏
      this.resultStr = "";
    },
    dataInitialize() {
      this.form.h_c0 = this.form1.h_c0;
      this.form.h_v = this.form1.h_v;
      this.form.h_h = this.form1.h_h;
      this.form.yl_b = this.form1.yl_b;
      this.form.yl_d = this.form1.yl_d;
      this.form.t_zb = this.form1.t_zb;
      this.form.err_dx = this.form1.err_dx;
      this.form.err_dy = this.form1.err_dy;
      this.form.yl_hc = this.form1.yl_hc;
      this.form.v_yl = this.form1.v_yl;
      this.form.h_yl = this.form1.h_yl;
      this.form.t_wdl = this.form1.t_wdl;
      this.form.r_t = this.form1.r_t;
      this.form.omiga_detle = this.form1.omiga_detle;
      this.form.lamda = this.form1.lamda;
      this.form.sl = this.form1.sl;
      this.form.f = this.form1.f;
      this.form.di = this.form1.di;
      this.form.dt = this.form1.dt;
      this.form.yl_yinxin = this.form1.yl_yinxin;
      this.form.qt_x00 = this.form1.qt_x00;
      this.form.qt_y00 = this.form1.qt_y00;
      this.form.qt_v0 = this.form1.qt_v0;
      this.form.qt_h0 = this.form1.qt_h0;
      this.form.ts0 = this.form1.ts0;
      this.form.ylbg_jl = this.form1.ylbg_jl;
      this.form.qt_xh = this.form1.qt_xh;
      this.form.flag_jidong = this.form1.flag_jidong;
      this.form.sl_gr = this.form1.sl_gr;
      this.form.gr_d = this.form1.gr_d;
      this.form.dfjs_gr = this.form1.dfjs_gr;
      this.form.gr_q = this.form1.gr_q;
      this.form.df_gr = this.form1.df_gr;
      this.form.flag_ganraoqi = this.form1.flag_ganraoqi;
      this.form.delta_t = this.form1.delta_t;
      this.form.s_hk = this.form1.s_hk;
      this.form.fz_num = this.form1.fz_num;
      this.form.hqsd = this.form1.hqsd;
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
    submitForm() {
      var dataFinal = {
        "h_c0": this.form.h_c0,
        "h_v": this.form.h_v,
        "h_h": this.form.h_h,
        "yl_b": this.form.yl_b,
        "yl_d": this.form.yl_d,
        "t_zb": this.form.t_zb,
        "err_dx": this.form.err_dx,
        "err_dy": this.form.err_dy,

        // 鱼雷弹道参数
        "yl_hc": this.form.yl_hc,
        "v_yl": this.form.v_yl,
        "h_yl": this.form.h_yl,
        "t_wdl": this.form.t_wdl,
        "r_t": this.form.r_t,
        "omiga_detle": this.form.omiga_detle,

        // 鱼雷自导参数
        "lamda": this.form.lamda,
        "sl": this.form.sl,
        "f": this.form.f,
        "di": this.form.di,
        "dt": this.form.dt,
        "yl_yinxin": this.form.yl_yinxin,

        // 潜艇参数
        "qt_x00": this.form.qt_x00,
        "qt_y00": this.form.qt_y00,
        "qt_v0": this.form.qt_v0,
        "qt_h0": this.form.qt_h0,
        "ts0": this.form.ts0,
        "ylbg_jl": this.form.ylbg_jl,

        // 潜艇机动参数
        "qt_xh": this.form.qt_xh,
        "flag_jidong": this.form.flag_jidong,

        // 干扰器参数
        "sl_gr": this.form.sl_gr,
        "gr_d": this.form.gr_d,
        "dfjs_gr": this.form.dfjs_gr,
        "gr_q": this.form.gr_q,
        "df_gr": this.form.df_gr,
        "flag_ganraoqi": this.form.flag_ganraoqi,

        // 仿真控制
        "delta_t": this.form.delta_t,
        "s_hk": this.form.s_hk,
        "fz_num": this.form.fz_num,

        "hqsd": this.form.hqsd,
      };
      this.form1 = dataFinal;
      this.connectWebSocket(dataFinal)
    },
    finishComp(){
      // 停止计算时只发送必要的停止消息，不要包含所有表单数据
      var stopMessage = {
        "type": "stop_calculation"
      };

      this.sendStopMessage(stopMessage)
    },

// 专门发送停止消息的方法
    sendStopMessage(stopMessage) {
      console.log("发送停止消息:", stopMessage)

      // 直接发送停止消息，不设置onmessage回调
      this.socket.send(JSON.stringify(stopMessage))

      // 单独处理停止的响应
      const originalOnMessage = this.socket.onmessage;
      this.socket.onmessage = (event) => {
        const data = JSON.parse(event.data)
        console.log("停止响应:", data)

        if (data.type === "status" && data.message === "计算已停止") {
          // 停止成功，恢复原来的消息处理器
          this.socket.onmessage = originalOnMessage;
          this.$message.success("计算已停止");
        }

        this.zantingList.push(data)
        console.log(this.zantingList)
      }
    },
    connectWebSocket(dataFinal) {
      console.log(dataFinal)
      // 创建WebSocket连接
      this.socket.send(JSON.stringify(dataFinal))
      this.socket.onmessage = (event) => {
        const data = JSON.parse(event.data)
        console.log(data)
        this.zantingList.push(data)
        console.log(this.zantingList)


        if(data.type=="progress"){
          this.zantingList.push(data.data)
        }else {
          this.zantingList.push(data)
        }

        this.dataFinal1.jsId = this.$route.query.id;
        if (this.currentImage != null && this.currentImage != "") {
          const reusltData = {
            ...dataFinal,
            "resultStr": this.resultStr,
            "finalHc": this.form.finalHc,
            "finalZD": this.form.finalZD,
          }
          this.dataFinal1.jsResult = JSON.stringify(reusltData);
        } else {
          const reusltData = {
            ...dataFinal,
            "result": this.form.result,
          }
          this.dataFinal1.jsResult = JSON.stringify(reusltData);
        }
        this.dataFinal1.allImg = this.currentImage;
      }

      this.socket.onclose = () => {
        console.log('WebSocket连接关闭')
      }
    },
    test() {
      this.form.h_c0 = 30.0;
      this.form.h_v = 60.0;
      this.form.h_h = 100.0;
      this.form.yl_b = 300.0;
      this.form.yl_d = 3000.0;
      this.form.t_zb = 3.0;
      this.form.err_dx = 0.1;
      this.form.err_dy = 30;
      this.form.yl_hc = 9400.0;
      this.form.v_yl = 42.0;
      this.form.h_yl = 100.0;
      this.form.t_wdl = 4.0;
      this.form.r_t = 100.0;
      this.form.omiga_detle = 6.0;
      this.form.lamda = 40.0;
      this.form.sl = 210.0;
      this.form.f = 30.0;
      this.form.di = 20.0;
      this.form.dt = 39.7;
      this.form.yl_yinxin = 30.0;
      this.form.qt_x00 = 0.0;
      this.form.qt_y00 = 0.0;
      this.form.qt_v0 = 4.0;
      this.form.qt_h0 = 120.0;
      this.form.ts0 = 15.0;
      this.form.ylbg_jl = 2000.0;
      this.form.qt_xh = 20.0;
      this.form.flag_jidong = 1;
      this.form.sl_gr = 181.0;
      this.form.gr_d = 200.0;
      this.form.dfjs_gr = 20.0;
      this.form.gr_q = 150.0;
      this.form.df_gr = 1.0;
      this.form.flag_ganraoqi = 0;
      this.form.delta_t = 1.0;
      this.form.s_hk = 3.0;
      this.form.fz_num = 0;

      this.form.hqsd = 0;
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
  watch: {
    zantingList: {
      handler(newList) {
        if (this.zanting==0 && newList.length > 0) {
          const data1 = this.zantingList[0]
          if (data1.type === 'update_hqsd') {
            this.resultStr = data1.str
          }
          else if (data1.type === 'chart_update') {
            this.currentImage = data1.image
            this.resultStr = data1.str
            this.form.finalHc = data1.finalHc
            this.form.finalZD = data1.finalZD
            if(this.form.finalZD != ""){
              this.form.finalZD = data1.finalZD
            }
          }
          else  if (data1.type === 'result_update') {
            this.currentImage = data1.image
            this.resultStr = data1.str
            this.form.finalHc = data1.finalHc
            this.form.finalZD = data1.finalZD
          }
          else if (data1.type === 'average_update') {
            this.form.result = data1.str
          }
          else if(data1.type === 'process'){
            if(data1.flag_mz==1){
              this.resultStr = "第"+(data1.numstr+1)+"次运行，鱼雷命中潜艇，用时"+data1.str+"秒"
            }else {
              this.resultStr = "第"+(data1.numstr+1)+"次运行，鱼雷未命中潜艇，用时"+data1.str+"秒"
            }
          }

          console.log(this.zantingList)

          setTimeout(() => {
            this.zantingList.shift(); // 1秒后删除
          }, 1000);
        }
      },
      deep: true, // 深度监听
    },
  },
  beforeDestroy() {
    if (this.socket) {
      this.socket.close();
    }
  },
  created() {
    // 连接 FastAPI WebSocket
    this.socket = new WebSocket('ws://127.0.0.1:9081/ws');

    this.socket.onopen = () => {
      console.log('WebSocket 已连接');
    };

    // this.socket.onmessage = (event) => {
    //   const data = JSON.parse(event.data);
    //   this.response = data;
    // };

    this.socket.onclose = () => {
      console.log('WebSocket 已关闭');
    };

    this.socket.onerror = (err) => {
      console.error('WebSocket 错误:', err);
    };
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

/deep/.el-checkbox__inner {
  width: 0.8vw;
  height: 0.8vw;
}

.selected-option {
  text-align: left;
  font-size: 0.7vw;
  display: flex;
  align-items: center;
  white-space: nowrap;
  margin-left: 0.7vw;
  width: 3vw;
  height: 100%;
  line-height: 4vh;
}

.options {
  border: 2px #00daff solid;
  width: 4.5vw;
  list-style: none;
  text-align: center;
  padding: 0;
  position: absolute;
  left: 18.4vw;
  top: 2vh;
  color: #fff;
  border-radius: 0.5vw;
  z-index: 99;
  font-size: 0.8vw;
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
  width: 100%;
  height: 100%;
  color: #fff;
  border: none;
  background-color: transparent;
}

/deep/.el-input {
  width: 4vw;
  height: 100%;
  font-size: 0;
  /* width: 80%; */
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

.xialakuang /deep/ .el-image {
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
  display: flex;
  align-items: center;
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
  background-size: 100% 100%;
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
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
}

.back1 {
  background-image: url('@/assets/img/back1.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
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
  height: 37vh;
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
  justify-content: space-between;
  width: 11.5vw;
  padding-left: 2vw;
  margin-bottom: 0.5vh;
}

.formaction1 {
  height: 3vh;
  display: flex;
  justify-content: space-between;
  width: 12.5vw;
  padding-left: 1vw;
  margin-bottom: 0.5vh;
}

.formaction2 {
  height: 3vh;
  display: flex;
  justify-content: space-between;
  width: 9.5vw;
  padding-left: 0.8vw;
  margin-bottom: 0.5vh;
}

.formaction-checkbox {
  height: 3vh;
  display: flex;
  width: 14.5vw;
  padding-left: 1vw;
  margin-bottom: 0.5vh;
  align-items: center;
}

.formaction-checkbox label {
  color: #fff;
  font-size: 0.8vw;
}

.formaction .el-input {
  display: flex;
  align-items: center;
  height: 100%;
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

.xialakuang /deep/ .el-image__inner {
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

#option1 {
  appearance: none;
  width: 0.8vw;
  height: 0.8vw;
  box-sizing: border-box;
  border: 1px solid #fff;
  /* border-radius: 50%; */
  position: relative;
  outline: none;
  cursor: pointer;
}

#option1::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #fff;
  /* border-radius: 50%; */
}

#option1:checked {
  background-color: #00daff;
  border-color: #00daff;
}

#option1:checked::before {
  transform: scale(0);
}

#option1:checked:after {
  /* 显示自定义的勾选标记 */
  content: '';
  position: absolute;
  left: 0.3vw;
  top: 0;
  width: 0.2vw;
  height: 0.5vw;
  border-style: solid;
  border-color: #fff;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
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

.formaction5 {
  height: 3vh;
  display: flex;
  width: 100%;
  margin-bottom: 2vh;
  justify-content: center;
}

.textArea .el-textarea {
  height: 24.5vh;
  font-size: 0.8vw;
}

.textArea /deep/.el-textarea__inner {
  height: 18%;
  border: none;
  color: #fff;
  background-color: transparent;
}

.waibiankuang {
  background-image: url('@/assets/img/wbk.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  padding-top: 2vh;
  padding-left: 1vw;
}

.inputbg {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.inputbg2 {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  background-color: lightsalmon;
}
</style>
