<template>
  <div class="background-container">
    <div class="content-container">
      <div
        style="display: flex;width: 100%;margin-bottom: 1vh;margin-top: 2vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color: #004e9c; font-size: 1.6vw;font-weight: 500;">
          海洋环境对声呐探测的影响分析软件
        </div>

        <!--        <el-button type="primary" class="button1" style="height: 1.5vw;margin-left: 33vw;" @click="save">保存</el-button>-->
      </div>
      <img style="height: 0.15vw;object-fit: contain;" src="@/assets/img/hengxian.png">
      <div style="width: 100%;height: 86%;display: flex;flex-direction: row;">
        <div class="box1">
          <div style="height: 35%;width: 100%;background-color: #006cda;border-radius: 1vw;">
            <div
              style="width: 99%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;margin-left: 0.5%;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 0.8%;">
              声速剖面参数设置
            </div>
            <div style="width: 94%;margin-left: 3%;display: flex;flex-direction: row;margin-top: 1%;">
              <div class="terrain-table" style="margin-left: 14%;height: 6vw;">
                <div style="width: 100%;text-align: center;color: #FFFFFF;font-size: 1vw;">声速剖面</div>
                <div class="tabnle" style="height: 100%;">
                  <table v-if="this.form.SeaDep == '浅海'">
                    <tbody>
                      <tr v-for="(item, index) in snTable1" :key="index">
                        <td class="leftTd" style="width: 8vw;">
                          <el-input style="width: 8vw;" type="text" v-model="snTable1[index]"   :max="200"
                                    oninput="if(value>200)value=200"/>
                        </td>
                        <td class="rightTd" style="width: 8vw;">
                          <el-input style="width: 8vw;" type="text" v-model="snTable2[index]" />
                        </td>
                      </tr>
                    </tbody>
                  </table>
                  <table v-if="this.form.SeaDep == '深海'">
                    <tbody>
                      <tr v-for="(item, index) in snTable1ss" :key="index">
                        <td class="leftTd" style="width: 8vw;">
                          <el-input style="width: 8vw;" type="text" v-model="snTable1ss[index]" />
                        </td>
                        <td class="rightTd" style="width: 8vw;">
                          <el-input style="width: 8vw;" type="text" v-model="snTable2ss[index]" />
                        </td>
                      </tr>
                    </tbody>
                  </table>

                </div>

              </div>
            </div>

          </div>
          <div style="height: 35%;width: 100%;background-color: #006cda;border-radius: 1vw;">
            <div
              style="width: 99%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;margin-left: 0.5%;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 0.8%;">
              计算参数设置
            </div>
            <div style="width: 94%;height: 1.8vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;">
              <div style="width: 50%;line-height: 1.8vw;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">距离上的初始最大值/m</div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.r2" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
            </div>
            <div style="width: 94%;height: 1.8vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;">
              <div style="width: 50%;line-height: 1.8vw;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">距离上的间隔/m</div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.delta_r" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
            </div>
            <div style="width: 94%;height: 1.8vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;">
              <div style="width: 50%;line-height: 1.8vw;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">接收器深度点数</div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.Nrd" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
            </div>
            <div style="width: 94%;height:1.8vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;">
              <div style="width: 50%;line-height: 1.8vw;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">深度的间隔/m</div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.delta_depth" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
            </div>
            <!-- <div style="width: 94%;height: 2vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;">
              <div style="width: 50%;line-height: 2vw;color: #Ffffff;font-size: 1vw;margin-left: 10%;">固定接收器距离点数</div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.Nrr" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
            </div>
            <div style="width: 94%;height: 2vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;">
              <div style="width: 50%;line-height: 2vw;color: #Ffffff;font-size: 1vw;margin-left: 10%;">固定点数</div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.num_points" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
            </div> -->
          </div>
          <div style="height: 26%;width: 100%;background-color: #006cda;border-radius: 1vw;">
            <div
              style="width: 99%;background-color:#004e9c;height: 2vw;border-radius: 0.6vw;margin-left: 0.5%;line-height: 2vw;font-size: 1vw;color: #Ffffff;text-align: center;margin-top: 1%">
              仿真控制</div>

            <div style="width: 100%;height: 90%;display: flex;flex-direction: row;margin-top: 2%;">
              <div style="height: 90%;width: 50%;display: flex;flex-direction: column;margin-left: 5%;">
                <div class="buttonLeft" style="display: inline-block;margin-left:1vw;width: 11vw;">
                  <el-button style="font-size: 0.8vw;" @click="test">载入测试值</el-button>
                </div>
                <div class="buttonLeft" style="display: inline-block;margin-left:1vw;width: 11vw;margin-top: 5%;">
                  <el-button style="font-size: 0.8vw;" @click="submitForm">计算</el-button>
                </div>
              </div>
              <div style="height: 90%;width: 50%;display: flex;flex-direction: column;margin-top: 5%;">
                <div class="buttonRight" style="width: 11vw;display: inline-block;">
                  <el-button style="font-size: 0.8vw;margin-left: -1vw;" @click="dataInitialize">数据初始化
                  </el-button>
                </div>

                <div class="buttonRight" style="width: 11vw;display: inline-block;margin-top: 5%;">
                  <el-button style="font-size: 0.8vw;margin-left: -1vw;" @click="clearImage">清除图片</el-button>
                </div>
              </div>
            </div>



          </div>
        </div>
        <div class="box2">
          <div style="display: flex;flex-direction: row;justify-content: space-between;height: 55%;">
            <div style="height: 100%;width: 30%;background-color: #006cda;border-radius: 1vw;">
              <div
                style="width: 99%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;margin-left: 0.5%;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 1%;">
                海底地形参数设置
              </div>
              <div class="formaction" style="width: 80%;margin-top: 4%;">
                <div class="text">类型</div>
                <div class="radioList" style="margin-top: 5%">
                  <div class="radio-group">
                    <label v-for="option in options" :key="option.label" class="radio-option">
                      <input type="radio" v-model="form.SeaDep" :value="option.label" class="radio-input"
                        @change="changeDP(form.SeaDep)">
                      <span class="radio-label">{{ option.label }}</span>
                    </label>
                  </div>
                </div>
              </div>
              <div class="formaction" style="width: 80%;margin-top: 4%;">
                <div class="text">地形</div>
                <div class="radioList" style="margin-top: 5%">
                  <div class="radio-group">
                    <label v-for="option in options1" :key="option.label" class="radio-option">
                      <input type="radio" v-model="form.SeaDx" :value="option.value" class="radio-input">
                      <span class="radio-label">{{ option.label }}</span>
                    </label>
                  </div>
                </div>
              </div>
              <div style="width: 94%;height: 2vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 4%;" v-if="this.form.SeaDx==0">
                <div class="terrain-table" style="margin-left: 15%;height: 8vw;">
                  <div style="width: 100%;text-align: center;color: #FFFFFF;font-size: 1vw;">地形参数</div>
                  <div class="tabnle" style="height: 100%;">
                    <table v-if="this.form.SeaDep == '浅海'">
                      <tbody>
                        <tr v-for="(item, index) in diTable1" :key="index">
                          <td class="leftTd">
                            <el-input type="text" v-model="diTable1[index]" />
                          </td>
                          <td class="rightTd">
                            <el-input type="text" v-model="diTable2[index]" :max="200"
                                      oninput="if(value>200)value=200"/>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                    <table v-if="this.form.SeaDep == '深海'">
                      <tbody>
                        <tr v-for="(item, index) in diTable1" :key="index">
                          <td class="leftTd">
                            <el-input type="text" v-model="diTable1ss[index]" />
                          </td>
                          <td class="rightTd">
                            <el-input type="text" v-model="diTable2ss[index]" />
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>

                </div>

              </div>
            </div>
            <div style="height: 100%;width: 30%;">
              <div style="height: 61%;width: 100%;background-color: #006cda;border-radius: 1vw;">
                <div
                  style="width: 99%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;margin-left: 0.5%;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 1%;">
                  海底地质参数设置
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">底部声速
                  </div>
                  <div class="inputbg" style="width: 30%;">
                    <el-input v-model="form.Bdry_Bot_cp" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">底部密度
                  </div>
                  <div class="inputbg" style="width: 30%;">
                    <el-input v-model="form.Bdry_Bot_rho" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">底部衰减
                  </div>
                  <div class="inputbg" style="width: 30%;">
                    <el-input v-model="form.Bdry_Bot_rholns" autocomplete="off" @focus="onFocus"
                      @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">海底s波速度
                  </div>
                  <div class="inputbg" style="width: 30%;">
                    <el-input v-model="form.Bdry_Bot_cs" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
              </div>
              <div style="height: 35%;width: 100%;background-color: #006cda;border-radius: 1vw;margin-top: 5%;">
                <div
                  style="width: 99%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;margin-left: 0.5%;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 1%;">
                  波束参数设置
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">声线数目
                  </div>
                  <div class="inputbg" style="width: 30%;">
                    <el-input v-model="form.Beam_Nbeams" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 10%;">波束张开角度/°
                  </div>
                  <div class="inputbg" style="width: 30%;">
                    <el-input v-model="form.alpha" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
              </div>
            </div>
            <div style="height: 100%;width: 30%;">
              <div style="height: 65%;width: 100%;background-color: #006cda;border-radius: 1vw;">
                <div
                  style="width: 99%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;margin-left: 0.5%;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 1%;">
                  吊放声呐参数设置
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div
                    style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 5%;white-space: nowrap;">
                    声呐发射声源级/dB</div>
                  <div class="inputbg" style="width: 30%;margin-left: 5%;">
                    <el-input v-model="form.SL" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 5%;">声源频率/Hz
                  </div>
                  <div class="inputbg" style="width: 30%;margin-left: 5%;">
                    <el-input v-model="form.freq" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 5%;">声源深度/km
                  </div>
                  <div class="inputbg" style="width: 30%;margin-left: 5%;">
                    <el-input v-model="form.Pos_s_depth" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 5%;">接收带宽/Hz
                  </div>
                  <div class="inputbg" style="width: 30%;margin-left: 5%;">
                    <el-input v-model="form.B" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 5%;">积分时间/s
                  </div>
                  <div class="inputbg" style="width: 30%;margin-left: 5%;">
                    <el-input v-model="form.TT" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 5%;">接收指向性指数
                  </div>
                  <div class="inputbg" style="width: 30%;margin-left: 5%;">
                    <el-input v-model="form.DI" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
              </div>
              <div style="height: 30%;width: 100%;margin-top: 4%;background-color: #006cda;border-radius: 1vw;">
                <div
                  style="width: 99%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;margin-left: 0.5%;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 1%;">
                  目标强度
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 5%;">目标入射舷角/rad
                  </div>
                  <div class="inputbg" style="width: 30%;margin-left: 5%;">
                    <el-input v-model="form.TS_alpha" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div style="width: 94%;height: 2.5vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 3%;">
                  <div style="width: 50%;line-height: 2.5vh;color: #Ffffff;font-size: 0.9vw;margin-left: 5%;">海况等级</div>
                  <div class="inputbg" style="width: 30%;margin-left: 5%;">
                    <el-input v-model="form.S" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
              </div>
            </div>
          </div>



          <div class="box3"
            style="display: flex;flex-direction: row;justify-content: space-between;margin-top: 1%;height: 44%">
            <div
              style="width: 48%;height: 100%;background-color: #006cda;border-radius: 1vw;display: flex;justify-content: center;justify-items: center;align-items: center;">
              <img :src="src" style="height: 96%;object-fit: contain;">
              <!--              <img src="@/assets/plot2.png" style="height: 96%;object-fit: contain;">-->
            </div>
            <div
              style="width: 48%;height: 100%;background-color: #006cda;border-radius: 1vw;display: flex;justify-content: center;justify-items: center;align-items: center;">
              <img :src="src1" style="height: 96%;object-fit: contain;">
              <!--              <img src="@/assets/plot2.png" style="height: 96%;object-fit: contain;">-->
            </div>
          </div>




        </div>

      </div>

      <div class="loader" v-if="showJZ"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: [
        { value: 0, label: '浅海' },
        { value: 1, label: '深海' },
      ],
      options1: [
        { value: 0, label: '地形参数' },
        { value: 1, label: '平坦' },
      ],
      bigUrl: "",
      showBig: false,
      urls: [],
      isVisible: true,
      isVisible1: false,
      isVisibleTiao: false,
      answerType: 0,
      showJZ: false,
      showOptions2: false,
      showOptions3: false,
      showOptions4: false,
      dataFinal1: {
        jsId: null,
        jsResult: {}
      },
      // snTable: [
      //   { range: 0, height: 1051.0 },
      //   { range: 0.8333333, height: 1080.6776 },
      //   { range: 1.666667, height: 1068.8258 },
      //   { range: 2.5, height: 1021.7262 },
      //   { range: 3.333333, height: 1016.1403 },
      //   { range: 3.333333, height: 1016.1403 },
      // ],

      //浅海
      // snTable1: [0, 20, 40, 60, 80, 100, 120, 140, 180, 200, 500],
      // snTable2: [1513, 1512.5, 1512, 1511, 1509, 1508.7, 1508.9, 1509.1, 1509.3, 1509.5, 1510.8],


      snTable1: [0, 20, 40, 60, 80, 100, 120, 140, 180, 200],
      snTable2: [1513, 1512.5, 1512, 1511, 1509, 1508.7, 1508.9, 1509.1, 1509.3, 1509.5],

      //深海    
      snTable1ss: [0, 200, 250, 400, 600, 800, 1000, 1200, 1400, 1600,
        1800, 2000, 2200, 2400, 2600, 2800, 3000, 3200, 3400,
        3600, 3800, 4000, 4200, 4400, 4600, 4800, 5000],
      // snTable1ss: [0, 200, 250, 400, 600, 800, 1000, 1200, 1400, 1600,
      //   1800, 2000],

      snTable2ss: [1548.52, 1530.29, 1526.69, 1517.78, 1509.49, 1504.30, 1501.38,
        1500.14, 1500.12, 1501.02, 1502.57, 1504.62, 1507.02, 1509.69,
        1512.55, 1515.56, 1518.67, 1521.85, 1525.10, 1528.38, 1531.70,
        1535.04, 1538.39, 1541.76, 1545.14, 1548.52, 1551.91],

      // snTable2ss: [1548.52, 1530.29, 1526.69, 1517.78, 1509.49, 1504.30, 1501.38,
      //   1500.14, 1500.12, 1501.02, 1502.57, 1504.62],

      byt1: [],
      byt2: [],
      sspmText1: [],
      sspmText2: [],

      // diTable1: [0, 10, 23, 25, 35, 50],
      // diTable2: [300, 320, 350, 400, 470, 500],

      diTable1: [0, 10, 23, 25, 35, 50],
      diTable2: [50, 100, 120, 150, 170, 200],


      diTable1ss: [0, 60, 70, 80, 100],
      diTable2ss: [5000, 4800, 500, 4800, 5000],
      src: '',
      src1: '',
      form: {
        delta_depth: 0,
        // z1: 0,
        // z2: 0,
        // c1: 0,
        // c2: 0,
        // c3: 0,
        SeaDep: "浅海",
        SeaDx:0,
        r2: 0,
        delta_r: 0,
        SL: 0,
        B: 0,
        TT: 0,
        DI: 0,
        TS_alpha: 0,
        S: 0,
        freq: 0,
        Pos_s_depth: 0,
        Beam_Nbeams: 0,
        alpha: 0,
        Bdry_Bot_cp: 0,
        Bdry_Bot_rho: 0,
        Bdry_Bot_rholns: 0,
        Bdry_Bot_cs: 0,
        Nrd: 0,
        Nrr: 0,
        num_points: 0,
      },
    };
  },
  methods: {
    changeDP(dep) {
      if (dep == "浅海") {
        this.byt1 = this.diTable1
        this.byt2 = this.diTable2
        this.sspmText1 = this.snTable1
        this.sspmText2 = this.snTable2
      } else {
        this.byt1 = this.diTable1ss
        this.byt2 = this.diTable2ss
        this.sspmText1 = this.snTable1ss
        this.sspmText2 = this.snTable2ss
      }
    },

    showBigInfo(src) {
      this.showBig = true;
      this.bigUrl = src;
    },
    clearImage() {
      this.src = "";
      this.src1 = "";
    },
    test() {
      if (this.form.SeaDep == "浅海") {
        this.byt1 = this.diTable1
        this.byt2 = this.diTable2
        this.sspmText1 = this.snTable1
        this.sspmText2 = this.snTable2
        this.form = {
          delta_depth: 1,
          r2: 50000,
          delta_r: 20,
          SL: 210,
          B: 1,
          TT: 0.025,
          DI: 6,
          TS_alpha: 20,
          S: 3,
          freq: 3000,
          Pos_s_depth: 200,
          Beam_Nbeams: 10,
          alpha: 20.3,
          Bdry_Bot_cp: 1600,
          Bdry_Bot_rho: 1.8,
          Bdry_Bot_rholns: 1,
          Bdry_Bot_cs: 0.8,
          Nrd: 1000,
          Nrr: 1000,
          num_points: 1000,
          SeaDep: '浅海',
          SeaDx: 0
        }
      }
      if (this.form.SeaDep == "深海") {
        this.byt1 = this.diTable1ss
        this.byt2 = this.diTable2ss
        this.sspmText1 = this.snTable1ss
        this.sspmText2 = this.snTable2ss
        this.form = {
          delta_depth: 200,
          r2: 100000,
          delta_r: 20,
          SL: 210,
          B: 1,
          TT: 0.025,
          DI: 6,
          TS_alpha: 20,
          S: 3,
          freq: 50,
          Pos_s_depth: 150,
          Beam_Nbeams: 500,
          alpha: 20.3,
          Bdry_Bot_cp: 1600.0,
          Bdry_Bot_rho: 1.8,
          Bdry_Bot_rholns: 1,
          Bdry_Bot_cs: 0.8,
          Nrd: 1000,
          Nrr: 501,
          num_points: 101,
          SeaDep: '深海',
          SeaDx: 0
        }
      }

    },
    onFocus(event) {
      const parentDiv = event.target.closest('.formaction');
      console.log(parentDiv)
      if (parentDiv) {
        const imagePath = require('@/assets/img/xuanzhongchang.png');
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
    onBlur1(event) {
      const parentDiv = event.target.closest('.formaction1');
      if (parentDiv) {
        parentDiv.style.backgroundImage = '';
      }
    },
    submitForm() {
      const processedSspm1 = this.sspmText1.filter(item => item !== "");
      const processedSspm2 = this.sspmText2.filter(item => item !== "");
      this.showJZ = true;
      var dataFinal = {
        "delta_depth": this.form.delta_depth,
        "r2": this.form.r2,
        "delta_r": this.form.delta_r,
        "freq": this.form.freq,
        "Pos_s_depth": this.form.Pos_s_depth,
        "Beam_Nbeams": this.form.Beam_Nbeams,
        "alpha": this.form.alpha,
        "Bdry_Bot_cp": this.form.Bdry_Bot_cp,
        "Bdry_Bot_rho": this.form.Bdry_Bot_rho,
        "Bdry_Bot_rholns": this.form.Bdry_Bot_rholns,
        "SL": this.form.SL,
        "B": this.form.B,
        "TT": this.form.TT,
        "DI": this.form.DI,
        "TS_alpha": this.form.TS_alpha,
        "S": this.form.S,
        "num_points": this.form.num_points,
        "Bdry_Bot_cs": this.form.Bdry_Bot_cs,

        "bty1": this.byt1,
        "bty2": this.byt2,

        "sspm1": processedSspm1,
        "sspm2": processedSspm2,
        "Nrd": this.form.Nrd,
        "Nrr": this.form.Nrr,
        "SeaDep": this.form.SeaDep,
        "SeaDx": this.form.SeaDx,
      }

      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9080/sn1",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {

          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res)

        this.urls.push(res.data.png4);
        this.urls.push(res.data.png5);

        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          method: "get",//get请求方式
          params: { urls: this.urls.join(",") },
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'GET',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          this.src = res.data.results[0].url;
          this.src1 = res.data.results[1].url;
          const combinedData = {
            ...this.form,
            ...this.urls
          };
          this.dataFinal1.jsResult = JSON.stringify(combinedData),
            this.dataFinal1.jsId = this.$route.query.id;
        })
      }
      ).finally(() => {
        this.showJZ = false;
      })
    },
    dataInitialize() {
      this.form.delta_depth = 0;
      this.form.z1 = 0;
      this.form.z2 = 0;
      this.form.c1 = 0;
      this.form.c2 = 0;
      this.form.c3 = 0;
      this.form.r2 = 0;
      this.form.delta_r = 0;
      this.form.freq = 0;
      this.form.Pos_s_depth = 0;
      this.form.Beam_Nbeams = 0;
      this.form.alpha = 0;
      this.form.Bdry_Bot_cp = 0;
      this.form.Bdry_Bot_rho = 0;
      this.form.Bdry_Bot_rholns = 0;
      this.form.SL = 0;
      this.form.B = 0;
      this.form.TT = 0;
      this.form.DI = 0;
      this.form.TS_alpha = 0;
      this.form.S = 0;
      this.form.SeaDx = 0;
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
    'form.ship_type'(newVal) {
      if (newVal == '055型') {
        this.heliList = [{
          id: 1,
          value: 'D',
          label: 'D'
        },
        {
          id: 2,
          value: 'E',
          label: 'E'
        },
        {
          id: 3,
          value: 'G',
          label: 'G'
        },
        {
          id: 4,
          value: 'F',
          label: 'F'
        }]
      } else {
        this.heliList = [{
          id: 1,
          value: 'D',
          label: 'D'
        },
        {
          id: 2,
          value: 'E',
          label: 'E'
        },
        {
          id: 3,
          value: 'G',
          label: 'G'
        }]
      }
    },
    'form.heli_type'(newVal) {
      if (newVal == 'D') {
        this.form.zjsb = '鱼叉';
      } else if (newVal == 'E') {
        this.form.zjsb = '鱼叉';
      } else if (newVal == 'G') {
        this.form.zjsb = '助降网';
      } else {
        this.form.zjsb = '拉降系统';
      }
    }
  },
};
</script>

<style scoped>
.background-container {
  padding: 0px;
  width: 98.5%;
  height: 95.2%;
  background-color: #fff;
  /* 设置为视口高度 */
  background-size: cover;
  background-position: center;
  overflow: hidden;
  /* 隐藏超出背景图的内容 */
  margin-left: 1.2%;
  margin-top: 2.5%;
  border-radius: 1vw;
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
  width: 100%;
  height: 100%;
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
  color: #fff;
  border: none;
  background-color: transparent;
}

/deep/ .el-input {
  width: 4vw;
  height: 100%;
  font-size: 0;
  /* width: 80%; */
}

.buttonLeft .el-button {
  width: 8vw;
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
  width: 8vw;
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


.back4 /deep/ .el-image__inner {
  border-radius: 1vw;
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
  width: 24vw;
  padding-left: 3vw;
  margin-bottom: 0.5vh;
}

.formaction1 {
  height: 3vh;
  display: flex;
  justify-content: space-between;
  width: 20vw;
  padding-left: 3vw;
  margin-bottom: 0.5vh;
  position: relative;
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

.loader {
  border: 5px solid #f3f3f3;
  border-top: 5px solid #3498db;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  animation: spin 2s linear infinite;
  margin: 20px auto;
  position: fixed;
  top: 50%;
  left: 50%;
  z-index: 9999;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

.waibiankuang {

  background-size: 100% 100%;
  padding-top: 2vh;
  padding-left: 1vw;
}

.terrain-table {
  padding-bottom: 0.8vh;
  height: 4vw;
}

.tabnle {
  padding-bottom: 0.8vh;
  height: 5vw;
  overflow-y: scroll;
}

.tabnle::-webkit-scrollbar {
  width: 5px;
  height: 3px;
}

.tabnle::-webkit-scrollbar-thumb {
  background-color: #03f7f7;
  border-radius: 10px;
}

.tabnle::-webkit-scrollbar-track {
  background: transparent;
}

.tabnle::-webkit-scrollbar-button {
  display: none;
}

.terrain-table table {
  padding-bottom: 0.5vh;
  width: 100%;
  border-top: 1px solid #0e6fdd;
  border-collapse: collapse;
}

.terrain-table tr {
  width: 100%;
}

.terrain-table th,
.terrain-table td {
  color: #fff;
  font-size: 0.7vw;
  width: 50%;
  text-align: center;
  vertical-align: middle;
  height: 1vh;
  /* 匹配输入框高度 */
  align-items: center;
}


.rightTd /deep/ .el-input__inner {
  /* text-align: right; */
  width: 100%;
}

.rightTd /deep/ .el-input {
  width: 5vw;
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.leftTd /deep/ .el-input {
  width: 5vw;
  text-align: center;
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.inputbg .el-input {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  width: 100%;
}

.radio-group {
  width: 80%;
  height: 100%;
  display: flex;
  justify-content: space-around;


}


.radio-option {
  display: flex;
  align-items: center;
  cursor: pointer;

}


.radio-input {
  appearance: none;
  width: 0.8vw;
  height: 0.8vw;
  border: 2px solid #23f9fd;
  border-radius: 50%;
  margin-right: 0.5vw;
  position: relative;
  cursor: pointer;
  transition: all 0.2s;
}

.radio-input:checked {
  border: none;
}

.radio-input:checked::after {
  content: '';
  position: absolute;
  width: 0.8vw;
  height: 0.8vw;


  background: #23f9fd;
  border-radius: 50%;
}

.radio-label {
  font-size: 0.8vw;
  color: #FFFFFF;
  white-space: nowrap;
}

.radioList {
  height: 10%;
  width: 100%;
  position: relative;
}

.box1 {
  width: 30%;
  height: 100%;
  margin-left: 2.5%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

}

.buttonRight .el-button {
  width: 8vw;
  height: 2vh;
  margin-left: 1vw;
  line-height: 0.6vh;
  display: block;
  border-radius: 0;
  font-size: 0.7vw;
  background-color: transparent;
  border: none;
  color: #fff;
}

.buttonLeft .el-button {
  width: 8vw;
  height: 2vh;
  margin-left: 1vw;
  line-height: 0.6vh;
  display: block;
  border-radius: 0;
  font-size: 0.7vw;
  background-color: transparent;
  border: none;
  color: #fff;
}


.box2 {
  width: 62%;
  height: 100%;
  margin-left: 2.5%;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  ;

}

.box3 {
  width: 100%;
  height: 43%;
  border-radius: 1vw;


}
</style>
