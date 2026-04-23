<template>
  <div class="background-container">
    <div class="content-container">
      <div
        style="display: flex;width: 96%;margin-left: 14vw;margin-bottom: 1.5vh;margin-top: 1.5vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color: #fff; font-size: 1.6vw;font-weight: 500;">
          大气环境对雷达探测的影响分析软件
        </div>
        <el-button type="primary" class="button1" style="height: 1.5vw;margin-left: 2vw;"
          @click="test">载入初始值</el-button>
        <el-button type="primary" class="button1" style="height: 1.5vw;"
          @click="dataInitialize">数据初始化</el-button>
        <el-button type="primary" class="button1" style="height: 1.5vw;" @click="clear">数据清除</el-button>
        <el-button type="primary" class="button1" style="height: 1.5vw;" @click="submitForm">计算</el-button>
<!--        <el-button type="primary" class="button1" style="height: 1.5vw;" @click="save">保存</el-button>-->
      </div>
      <div style="display: flex;width: 98%;width: 96.5%;height: 87%;flex-direction: column;" class="waibiankuang">
        <div class="inputBox">
          <div class="box1" style="height: 42.5vh;margin-bottom: 1vh;">
            <div class="hg">
              <div class="smallTitle">
                <div class="baiquan"></div>
                <div class="baititle" style="white-space: nowrap;">雷达参数设置</div>
              </div>
            </div>
            <div class="boxSr1">
              <div class="twoInput">
                <div class="leftInput">
                  <div class="leftTitle">发射功率(kW)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入"
                      v-model="form.transmitterPower" />
                  </div>
                </div>
                <div class="rightInput">
                  <div class="rightTitle">工作频率(MHz)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入"
                      v-model="form.frequency" />
                  </div>
                </div>
              </div>
              <div class="twoInput">
                <div class="leftInput">
                  <div class="leftTitle">脉冲宽度(μs)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入"
                      v-model="form.pulseWidth" />
                  </div>
                </div>
                <div class="rightInput">
                  <div class="rightTitle">发射天线增益(dB)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入"
                      v-model="form.transmitAntennaGain" />
                  </div>
                </div>
              </div>
              <div class="twoInput">
                <div class="leftInput">
                  <div class="leftTitle">接收天线增益(dB)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入"
                      v-model="form.receiveAntennaGain" />
                  </div>
                </div>
                <div class="rightInput">
                  <div class="rightTitle">接收天线副瓣(dB)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入"
                      v-model="form.receiveAntennaSidelobe" />
                  </div>
                </div>
              </div>
              <div class="twoInput">
                <div class="leftInput">
                  <div class="leftTitle">噪声系数(dB)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入"
                      v-model="form.noiseFigure" />
                  </div>
                </div>
                <div class="rightInput">
                  <div class="rightTitle">系统损耗(dB)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入" v-model="form.losses" />
                  </div>
                </div>
              </div>
              <div class="twoInput">
                <div class="leftInput">
                  <div class="leftTitle">脉冲重复频率(Hz)</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 80%;text-indent: 40px;" type="text" placeholder="请输入" v-model="form.prf" />
                  </div>
                </div>
                <div class="rightInput">
                  <div class="rightTitle">检测概率(&lt;1):</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.probabilityOfDetection" />
                  </div>
                </div>
              </div>
              <div class="twoInput">
                <div class="leftInput">
                  <div class="leftTitle">虚警概率(&lt;1):</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.probabilityOfFalseAlarm" />
                  </div>
                </div>
                <div class="rightInput">
                  <div class="rightTitle">多普勒滤波器带宽(Hz):</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入多普勒滤波器带宽"
                      v-model="form.dopplerFilterBandwidth" />
                  </div>
                </div>
              </div>
              <div class="twoInput">
                <div class="leftInput">
                  <div class="leftTitle">频率捷变带宽(MHz):</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.frequencyAgilityBandwidth" />
                  </div>
                </div>
                <div class="rightInput">
                  <div class="rightTitle">水平波束宽度(°):</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.azimuthBeamwidth" />
                  </div>
                </div>
              </div>
              <div class="twoInput">
                <div class="leftInput">
                  <div class="leftTitle">天线转速(°/s):</div>
                  <div class="password-input-container">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.azimuthScanRate" />
                  </div>
                </div>
                <div class="rightInput">

                </div>
              </div>
            </div>
          </div>
          <div class="box1" style="overflow-y: scroll;height: 42.5vh;margin-bottom: 1vh;">
            <div class="hg">
              <div class="smallTitle">
                <div class="baiquan"></div>
                <div class="baititle" style="white-space: nowrap;">干扰参数设置</div>
              </div>
            </div>
            <div class="radioList1">
              <div class="radio-group1">
                <div style="font-size: 0.75vw;color: #FFFFFF">请选择干扰类型:</div>
                <label v-for="option in options1" :key="option.value" class="radio-option1">
                  <input type="radio" v-model="form.jammingType" :value="option.value" class="radio-input1">
                  <span class="radio-label1">{{ option.label }}</span>
                </label>
              </div>
            </div>
            <div class="ylgr" v-if="this.form.jammingType == 0 || this.form.jammingType == 3">
              <div class="smallJian">
                <img style="height: 0.8vw;object-fit: contain;" src="../../assets/img/baogaojian.png">
                <div class="smallJianFont">远离干扰参数</div>
              </div>
              <div class="yjlsl">
                <div class="grsl">干扰数量：</div>
                <div class="password-input-containergr">
                  <img src="../../assets/img/grnum.png"
                    style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                  <input style="width: 95%;text-align: center;font-size: 0.9vw;" type="text" placeholder="请输入"
                    @input="updateTableData" v-model="form.num_jams" />
                </div>
              </div>
              <div class="grsj">

                <table class="tableInputOne" v-if="form.num_jams > 0">
                  <thead class="theaderInfo" style="height: 2vw;font-size: 0.8vw;font-weight: normal">
                    <tr style="color: #FFFFFF;font-weight: normal;">
                      <th style="border-top-left-radius: 1vw;border-bottom-left-radius:1vw; ">{{ columns[0].label }}
                      </th>
                      <th v-for="(col, index) in columns.slice(1, -1)" :key="index">{{ col.label }}
                      </th>
                      <th style="border-top-right-radius: 1vw;border-bottom-right-radius:1vw; ">{{
                        columns[columns.length - 1].label }}</th>
                    </tr>
                  </thead>
                  <tbody style="margin-top: 2vw;">
                    <tr v-for="(row, rowIndex) in tableData" :key="rowIndex">
                      <td v-for="(col, colIndex) in columns" :key="colIndex" style="position: relative;height: 2vw;">
                        <div style="width: 100%;height: 100%;">
                          <input style="text-align: center" v-model="row[col.prop]">
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>

              </div>
            </div>

            <div class="zwgr" v-if="this.form.jammingType == 1 || this.form.jammingType == 3">
              <div class="smallJian">
                <img style="height: 0.8vw;object-fit: contain;" src="../../assets/img/baogaojian.png">
                <div class="smallJianFont">自卫干扰参数</div>
              </div>
              <div class="zwgrcs">
                <div class="oneInputzw">
                  <div class="oneLeftTitle">
                    干扰机功率:
                  </div>
                  <div class="password-input-container1">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.SSJ_pwr_jam" />
                  </div>
                </div>
                <div class="oneInputzw">
                  <div class="oneLeftTitle">
                    干扰机增益:
                  </div>
                  <div class="password-input-container1">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.SSJ_gain_dB" />
                  </div>
                </div>
                <div class="oneInputzw">
                  <div class="oneLeftTitle">
                    干扰机带宽:
                  </div>
                  <div class="password-input-container1">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.SSJ_bw" />
                  </div>
                </div>
                <div class="oneInputzw">
                  <div class="oneLeftTitle">
                    干扰机系统损失:
                  </div>
                  <div class="password-input-container1">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.SSJ_loss_dB" />
                  </div>
                </div>
              </div>
            </div>


          </div>
          <div class="box1" style="height: 24vh;">
            <div class="hg">
              <div class="smallTitle">
                <div class="baiquan"></div>
                <div class="baititle" style="white-space: nowrap;">目标参数设置</div>
              </div>

            </div>
            <div class="boxSr2">
              <div class="oneInput3">
                <div class="oneLeftTitle">
                  目标截面积(m²):
                </div>
                <div class="password-input-container1">
                  <img src="../../assets/img/dqjsInput.png"
                    style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                  <input style="width: 100%;text-indent: 40px;" type="text" v-model="form.rcs" />
                </div>
              </div>
              <div class="oneInput3">
                <div class="oneLeftTitle">
                  目标高度(°):
                </div>
                <div class="password-input-container1">
                  <img src="../../assets/img/dqjsInput.png"
                    style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                  <input style="width: 100%;text-indent: 40px;" type="text" v-model="form.elevationOfTarget" />
                </div>
              </div>
              <div class="oneInput3">
                <div class="oneLeftTitle">
                  目标长度(m):
                </div>
                <div class="password-input-container1">
                  <img src="../../assets/img/dqjsInput.png"
                    style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                  <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入多普勒滤波器带宽"
                    v-model="form.lengthOfTarget" />
                </div>
              </div>
            </div>

          </div>
          <div style="display: flex;width: 48%;height: 24vh;flex-direction: column;">
            <div class="box1" style="height: 100%;width: 100%;">
              <div class="hg">
                <div class="smallTitle">
                  <div class="baiquan"></div>
                  <div class="baititle" style="white-space: nowrap;">天气参数设置</div>
                </div>

              </div>
              <div class="radioList">
                <div class="radio-group">
                  <label v-for="option in options" :key="option.value" class="radio-option">
                    <input type="radio" v-model="form.useType" :value="option.value" class="radio-input">
                    <span class="radio-label">{{ option.label }}</span>
                  </label>
                </div>
              </div>

              <div class="boxSr3">
                <div class="oneInput3" v-if="form.useType == 1">
                  <div class="oneLeftTitle">
                    降雨量(mm/h):
                  </div>
                  <div class="password-input-container1">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.rainFallRate" />
                  </div>
                </div>
                <div class="oneInput3" v-if="form.useType == 2">
                  <div class="oneLeftTitle">
                    降雪量(mm/h):
                  </div>
                  <div class="password-input-container1">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.rainFallRate" />
                  </div>
                </div>
                <div class="oneInput3" v-if="form.useType == 3">
                  <div class="oneLeftTitle">
                    密度(g/m³):
                  </div>
                  <div class="password-input-container1">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率"
                      v-model="form.rainFallRate" />
                  </div>
                </div>
                <div class="oneInput3" v-if="form.useType == 3">
                  <div class="oneLeftTitle">
                    温度(°C):
                  </div>
                  <div class="password-input-container1">
                    <img src="../../assets/img/dqjsInput.png"
                      style="position: absolute;z-index: -1;width: 100%;height: 100%;">
                    <input style="width: 100%;text-indent: 40px;" type="text" placeholder="请输入检测概率" v-model="form.T" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>


        <div class="resultBox" v-if="showResultTable" id="capture">
          <!-- <div class="resultInput">
            <div class="resultJianTop">
              <img src="../../assets/img/resultPicJian.png"
                style="height: 100%;object-fit:contain;position: absolute;z-index: 100;">
              <div class="resultName">雷达参数</div>
            </div>
            <div class="resultLdList">
              <div class="oneLine">
                <div class="resultSmallBox" v-for="(param, index) in radarParams" :key="index">
                  <div class="smallTop">
                    <div class="smallIconInfo"></div>
                    <div class="smallIconFont">{{ param.name }}:</div>
                  </div>
                  <div class="smallDown">
                    <span style="color: #FFFFFF;margin-right: 1%;">{{ param.value }}</span><span
                      style="color: #50e8ff">{{ param.unit }}</span>
                  </div>
                </div>


              </div>
              <div class="oneLine">
                <div class="resultSmallBox" v-for="(param, index) in radarParams1" :key="index">
                  <div class="smallTop">
                    <div class="smallIconInfo"></div>
                    <div class="smallIconFont">{{ param.name }}:</div>
                  </div>
                  <div class="smallDown">
                    <span style="color: #FFFFFF;margin-right: 1%;">{{ param.value }}</span><span
                      style="color: #50e8ff">{{ param.unit }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="resultInput1">
            <div class="resultJianTop1">
              <img src="../../assets/img/resultPicJian.png"
                style="height: 100%;object-fit:contain;position: absolute;z-index: 100;">
              <div class="resultName">目标和环境参数</div>
            </div>
            <div class="resultHjList" v-if="this.form.useType != 3">
              <div class="HjInfo" v-for="(param, index) in targetParams" :key="index">
                <div class="HjTop">{{ param.name }}</div>
                <div class="HjDown">
                  <span style="font-size: 1.2vw;margin-bottom: 3%;font-weight: bold;margin-right: 2%;">{{
                    param.value
                  }}</span><span style="font-size: 0.8vw;margin-right: 2%;">{{ param.unit }}</span>
                </div>
              </div>

            </div>
            <div class="resultHjList" v-if="this.form.useType == 3">
              <div class="HjInfo1" v-for="(param, index) in targetParams" :key="index">
                <div class="HjTop">{{ param.name }}</div>
                <div class="HjDown">
                  <span style="font-size: 1.2vw;margin-bottom: 4%;font-weight: bold;margin-right: 2%;">{{
                    param.value
                  }}</span><span style="font-size: 0.8vw;margin-right: 5%;">{{ param.unit }}</span>
                </div>
              </div>

            </div>
          </div> -->
          <div class="resultInput2">
            <div class="resultJianTop2">
              <img src="../../assets/img/resultPicJian.png"
                style="height: 100%;object-fit:contain;position: absolute;z-index: 100;">
              <div class="resultName">无干扰情况下的检测距离</div>
            </div>
            <div class="resultTabl1">
              <table class="tableOne">
                <thead class="theaderInfo">
                  <tr>
                    <th class="first-header" style="color: #FFFFFF;font-size: 0.9vw;background-color: transparent">
                      Swerling
                      Case
                    </th>

                    <th :key="index" v-for="(item, index) in detectionRanges.slice(0, -1)">

                      <div class="case-header">{{ item.case }}</div>
                    </th>
                    <th class="last-header" style="color: #FFFFFF;font-size: 0.9vw;background-color: transparent">
                      {{ detectionRanges[detectionRanges.length - 1].case }}
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>
                      <div class="tableL1"> 大气衰减（dB）</div>
                    </td>
                    <td v-for="(item, index) in detectionRanges" :key="'atmos' + index">
                      <div class="infoList1">{{ item.atmos }}</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1" v-if="this.form.useType == 1">
                        降雨衰减（dB）
                      </div>
                      <div class="tableL1" v-if="this.form.useType == 2">
                        降雪衰减（dB）
                      </div>
                      <div class="tableL1" v-if="this.form.useType == 3">
                        云雾衰减（dB）
                      </div>
                    </td>
                    <td v-for="(item, index) in detectionRanges" :key="'rain' + index">
                      <div class="infoList1">{{ item.rain }}</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1">
                        检测距离（nm）
                      </div>
                    </td>
                    <td v-for="(item, index) in detectionRanges" :key="'range' + index">
                      <div class="infoList1">{{ item.range }}</div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>


          <!-- <div class="resultInput3" v-if="this.chooseNum == 0 || this.chooseNum == 3">
            <div class="resultJianTop3">
              <img src="../../assets/img/resultPicJian.png"
                style="height: 100%;object-fit:contain;position: absolute;z-index: 100;">
              <div class="resultName">远距干扰数据(干扰机数量: {{ jammerCount }})</div>
            </div>
            <div class="resultTabl3">
              <table class="tableOne">
                <thead class="theaderInfo">
                  <tr>
                    <th class="first-header" style="font-size: 0.8vw;">参数</th>
                    <th v-for="n in jammerCount - 1" :key="n">
                      <div class="case-header" style="font-size: 0.8vw;height: 2vw;">干扰机{{ n }}</div>
                    </th>
                    <th class="last-header" style="color: #FFFFFF;font-size: 0.8vw;background-color: transparent">
                      干扰机{{ jammerCount }}
                    </th>
                  </tr>
                </thead>
                <tbody style="font-size: 1vw;">
                  <tr>
                    <td style="width: 15%">
                      <div class="tableL1" style="font-size: 0.8vw;height: 65%;">干扰功率</div>
                    </td>
                    <td v-for="(pwr, index) in jammerValues[0]" :key="index" style="font-size: 0.8vw;">
                      <div class="infoList1">{{ pwr }}W</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1" style="font-size: 0.8vw;height: 65%;">干扰天线增益</div>
                    </td>
                    <td v-for="(gain, index) in jammerValues[1]" :key="index" style="font-size: 0.8vw;">
                      <div class="infoList1">{{ gain }}dB</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1" style="font-size: 0.8vw;height: 65%;">干扰带宽</div>
                    </td>
                    <td v-for="(bw, index) in jammerValues[2]" :key="index" style="font-size: 0.8vw;">
                      <div class="infoList1">{{ bw }}MHz</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1" style="font-size: 0.8vw;height: 65%;">干扰距离</div>
                    </td>
                    <td v-for="(range, index) in jammerValues[3]" :key="index" style="font-size: 0.8vw;">
                      <div class="infoList1">{{ range }}n.m</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1" style="font-size: 0.8vw;height: 65%;">干扰高度</div>
                    </td>
                    <td v-for="(height, index) in jammerValues[4]" :key="index" style="font-size: 0.8vw;">
                      <div class="infoList1">{{ height }}英尺</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1" style="font-size: 0.8vw;height: 65%;">干扰损耗</div>
                    </td>
                    <td v-for="(loss, index) in jammerValues[5]" :key="index" style="font-size: 0.8vw;">
                      <div class="infoList1">{{ loss }}dB</div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div> -->



          <!-- <div class="resultInput4" v-if="this.chooseNum == 1 || this.chooseNum == 3">
            <div class="resultJianTop4">
              <img src="../../assets/img/resultPicJian.png"
                style="height: 100%;object-fit:contain;position: absolute;z-index: 100;">
              <div class="resultName">自卫干扰数据</div>
            </div>
            <div class="resultHjList">
              <div class="HjInfo" v-for="(param, index) in selfJammerData" :key="index">
                <div class="HjTop">{{ param.name }}</div>
                <div class="HjDown">
                  <span style="font-size: 1.2vw;margin-bottom: 3%;font-weight: bold;margin-right: 2%;">{{
                    param.value
                  }}</span><span style="font-size: 0.8vw;margin-right: 2%;">{{ param.unit }}</span>
                </div>
              </div>

            </div>

          </div> -->


          <div class="resultInput2" v-if="this.chooseNum == 0 || this.chooseNum == 3 || this.chooseNum == 1">
            <div class="resultJianTop2">
              <img src="../../assets/img/resultPicJian.png" style="height: 100%;object-fit:contain;position: absolute;z-index: 100;">
              <div class="resultName">干扰情况下的检测距离</div>
            </div>
            <div class="resultTabl1">
              <table class="tableOne">
                <thead class="theaderInfo">
                  <tr>
                    <th class="first-header" style="color: #FFFFFF;font-size: 0.9vw;background-color: transparent">
                      Swerling
                      Case
                    </th>

                    <th :key="index" v-for="(item, index) in jammedDetectionRanges.slice(0, -1)">
                      <div class="case-header">{{ item.case }}</div>
                    </th>
                    <th class="last-header" style="color: #FFFFFF;font-size: 0.9vw;background-color: transparent">
                      {{ jammedDetectionRanges[jammedDetectionRanges.length - 1].case }}
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>
                      <div class="tableL1"> 大气衰减（dB）</div>
                    </td>
                    <td v-for="(item, index) in jammedDetectionRanges" :key="'atmos' + index">
                      <div class="infoList1">{{ item.atmos }}</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1" v-if="this.form.useType == 1">
                        降雨衰减（dB）
                      </div>
                      <div class="tableL1" v-if="this.form.useType == 2">
                        降雪衰减（dB）
                      </div>
                      <div class="tableL1" v-if="this.form.useType == 3">
                        云雾衰减（dB）
                      </div>
                    </td>
                    <td v-for="(item, index) in jammedDetectionRanges" :key="'rain' + index">
                      <div class="infoList1">{{ item.rain }}</div>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="tableL1">
                        干扰距离（nm）
                      </div>
                    </td>
                    <td v-for="(item, index) in jammedDetectionRanges" :key="'range' + index">
                      <div class="infoList1">{{ item.range }}</div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
        <!-- <div v-if="showResultTable" class="baocun" @click="save">保存</div> -->
      </div>
    </div>
  </div>
</template>

<script>


import html2canvas from "html2canvas";
import { fileUpdate } from "@/api/file";
import { saveJsResult } from "@/api/baogao";


export default {
  data() {
    return {
      showResultTable: false,
      columns: [
        { prop: 'name', label: '干扰机名称' },
        { prop: 'Power', label: '干扰机功率' },
        { prop: 'Gain', label: '干扰机天线增益' },
        { prop: 'Bandwidth', label: '干扰机宽带' },
        { prop: 'Range', label: '干扰机距离' },
        { prop: 'Height', label: '干扰机高度' },
        { prop: 'Loss', label: '干扰机系统损耗' }
      ],

      selectedOption: '',
      options: [
        { value: 1, label: '降雨' },
        { value: 2, label: '降雪' },
        { value: 3, label: '云和雾' }
      ],
      options1: [
        { value: 0, label: '远距离干扰' },
        { value: 1, label: '自卫干扰' },
        { value: 3, label: '远离和自卫干扰' },
        { value: 2, label: '无干扰' },
      ],
      isVisible: true, //雷达参数1
      isVisible1: false, //雷达参数2
      isVisible2: false, //天气参数
      isVisible3: false, //选择干扰
      isVisible4: false, //自卫干扰参数
      isVisible5: false,//远距离干扰
      isVisible6: false,//干扰机参数
      isVisible7: false,//降雨天气参数
      isVisible8: false,//降雪天气参数
      isVisible9: false,//云和雾天气参数
      title6: "干扰机参数",
      tableData: [
      ], // 表格数据


      chooseNum: 3,
      el_form_title: "",
      form: {
        transmitterPower: 4000,
        frequency: 3000,
        pulseWidth: 6.5,
        transmitAntennaGain: 36,
        receiveAntennaGain: 40,
        receiveAntennaSidelobe: 10,
        noiseFigure: 4.5,
        losses: 12,
        prf: 250,

        probabilityOfDetection: 0.90,
        probabilityOfFalseAlarm: 1e-6,
        dopplerFilterBandwidth: 250,
        frequencyAgilityBandwidth: 200,
        azimuthBeamwidth: 1.1,
        azimuthScanRate: 36,


        rcs: 1.0,
        elevationOfTarget: 0.4,
        lengthOfTarget: 10,
        rainFallRate: 0.0,

        SOJ: undefined,
        SSJ: undefined,
        jammingType: 2,
        useType: 0,
        T: 0,


        //自卫干扰参数
        SSJ_pwr_jam: 10,
        SSJ_gain_dB: 0,
        SSJ_bw: 20,
        SSJ_loss_dB: 7,


        //远距离干扰
        num_jams: 0,


        //远距离干扰机参数
        Power: 2000,
        Gain: 5,
        Bandwidth: 200,
        Range: 50,
        Height: 20000,
        Loss: 7,


        //远距离参数数组
        yjlList: [],


        SOJ_pwr_jam: [],
        SOJ_gain_dB: [],
        SOJ_bw: [],
        jam_range: [],
        jam_height: [],
        SOJ_loss_dB: [],


      },
      nowNum: 1,
      form1: {

      },

      editMode: false,
      jammerCount: 2,
      mulu: [
        { id: 0, name: "知识图谱", info: "Graph" },
        { id: 1, name: "辅助决策", info: "BaoGao" },
        { id: 2, name: "图文资源", info: "TwInfo" },
        { id: 3, name: "视频资源", info: "SpInfo" },
        { id: 4, name: "动画显示", info: "DhInfo" },
        { id: 5, name: "数值计算", info: "JsInfo" },
        { id: 6, name: "帮助文档", info: "HelpInfo" }
      ],
      dataFinal: {},
      radarParams: [],
      radarParams1: [],
      targetParams: [],
      detectionRanges: [],
      jammerParams: [
        { name: '干扰功率', unit: 'W' },
        { name: '干扰天线增益', unit: 'dB' },
        { name: '干扰带宽', unit: 'MHz' },
        { name: '干扰距离', unit: 'n.m' },
        { name: '干扰高度', unit: '英尺' },
        { name: '干扰损耗', unit: 'dB' }
      ],
      jammerValues: [],
      selfJammerData: [],
      jammedDetectionRanges: [],
      dataFinal1: {
        jsId: null,
        jsResult: {},
        allImg: "",
      },

    };
  },
  methods: {

    updateTableData() {
      // 根据干扰源数量生成表格数据
      const num = this.form.num_jams;
      if (num < 0) {
        this.$message.error("干扰源数量不能为负数");
        this.form.num_jams = 0;
        this.tableData = [];
        return;
      }
      this.tableData = [];
      for (let c = 0; c < num; c++) {

        let ccc = {
          name: "干扰机" + (c + 1),
          Power: this.form.Power,
          Gain: this.form.Gain,
          Bandwidth: this.form.Bandwidth,
          Range: this.form.Range,
          Height: this.form.Height,
          Loss: this.form.Loss
        }
        this.tableData.push(ccc)

      }

    },
    test(){
      this.form.transmitterPower = 4000;
      this.form.frequency = 3000;
      this.form.pulseWidth = 6.5;
      this.form.transmitAntennaGain = 36;
      this.form.receiveAntennaGain = 40;
      this.form.receiveAntennaSidelobe = 10;
      this.form.noiseFigure = 4.5;
      this.form.losses = 12;
      this.form.prf = 250;

      this.form.probabilityOfDetection = 0.9;
      this.form.probabilityOfFalseAlarm = 0.000001;
      this.form.dopplerFilterBandwidth = 250;
      this.form.frequencyAgilityBandwidth = 200;
      this.form.azimuthBeamwidth = 1.1;
      this.form.azimuthScanRate = 36;


      this.form.rcs = 1;
      this.form.elevationOfTarget = 0.4;
      this.form.lengthOfTarget = 10;
      this.form.rainFallRate = 0;

      this.form.SOJ = undefined;
      this.form.SSJ = undefined;
      this.form.jammingType = 2;
      this.form.useType = 0;
      this.form.T = 0;


      //自卫干扰参数
      this.form.SSJ_pwr_jam = 10;
      this.form.SSJ_gain_dB = 0;
      this.form.SSJ_bw = 20;
      this.form.SSJ_loss_dB = 7;


      //远距离干扰
      this.form.num_jams = 0;


      //远距离干扰机参数
      this.form.Power = 2000;
      this.form.Gain = 5;
      this.form.Bandwidth = 200;
      this.form.Range = 50;
      this.form.Height = 20000;
      this.form.Loss = 7;


      //远距离参数数组
      this.form.yjlList = [];


      this.form.SOJ_pwr_jam = [];
      this.form.SOJ_gain_dB = [];
      this.form.SOJ_bw = [];
      this.form.jam_range = [];
      this.form.jam_height = [];
      this.form.SOJ_loss_dB = [];
      this.showResultTable = false;
    },
    submitForm() {
      // 处理表单提交
      this.chooseNum = this.form.jammingType;
      console.log(this.chooseNum)
      if (this.chooseNum == 0) {
        this.form.SOJ = 1
        this.form.SSJ = 0
        this.form.SOJ_pwr_jam = []
        this.form.SOJ_gain_dB = []
        this.form.SOJ_bw = []
        this.form.jam_range = []
        this.form.jam_height = []
        this.form.SOJ_loss_dB = []
        this.detectionRanges = []
        this.jammedDetectionRanges = []
        this.targetParams = []
        for (let a = 0; a < this.tableData.length; a++) {
          this.form.SOJ_pwr_jam.push(this.tableData[a].Power)
          this.form.SOJ_gain_dB.push(this.tableData[a].Gain)
          this.form.SOJ_bw.push(this.tableData[a].Bandwidth)
          this.form.jam_range.push(this.tableData[a].Range)
          this.form.jam_height.push(this.tableData[a].Height)
          this.form.SOJ_loss_dB.push(this.tableData[a].Loss)

        }
        var dataFinal = {
          "trans_pwr_radar": this.form.transmitterPower,
          "freq_radar": this.form.frequency,
          "pulse_width": this.form.pulseWidth,
          "GTDB_radar": this.form.transmitAntennaGain,
          "GRDB_radar": this.form.receiveAntennaGain,
          "GRDB_sl_radar": this.form.receiveAntennaSidelobe,
          "noise_fig_radar": this.form.noiseFigure,
          "loss_radar_dB": this.form.losses,
          "PRF": this.form.prf,

          "prob_det": this.form.probabilityOfDetection,
          "prob_false_alarm": this.form.probabilityOfFalseAlarm,
          "BW_dop": this.form.dopplerFilterBandwidth,
          "BW_fa": this.form.frequencyAgilityBandwidth,
          "Azimuth_bw": this.form.azimuthBeamwidth,
          "az_rate": this.form.azimuthScanRate,

          "RCS": this.form.rcs,
          "el_tgt_deg": this.form.elevationOfTarget,
          "target_length": this.form.lengthOfTarget,
          "rain_fall": this.form.rainFallRate,
          "T": this.form.T,
          "useType": this.form.useType,

          "SOJ": this.form.SOJ,
          "SSJ": this.form.SSJ,
          "num_jams": this.form.num_jams,

          //自卫干扰
          "SSJ_pwr_jam": this.form.SSJ_pwr_jam,
          "SSJ_gain_dB": this.form.SSJ_gain_dB,
          "SSJ_bw": this.form.SSJ_bw,
          "SSJ_loss_dB": this.form.SSJ_loss_dB,

          //远距离干扰
          "SOJ_pwr_jam": this.form.SOJ_pwr_jam,
          "SOJ_gain_dB": this.form.SOJ_gain_dB,
          "SOJ_bw": this.form.SOJ_bw,
          "jam_range": this.form.jam_range,
          "jam_height": this.form.jam_height,
          "SOJ_loss_dB": this.form.SOJ_loss_dB,


        }
        this.form1 = dataFinal;
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:9080/dqjy",//请求的后台接口
          method: "post",//get请求方式
          data: dataFinal,
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'POST',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)

          if (res.data != undefined) {
            //循环
            for (let a = 0; a < res.data.length; a++) {
              if (res.data[a]["num"] == 0) {
                //雷达参数1
                var Pt = res.data[a]["Pt(kw)"]
                var f = res.data[a]["f(Mhz)"]
                var PW = res.data[a]["PW(1e-6*s)"]
                var PRF = res.data[a]["PRF(pps)"]
                var Gt = res.data[a]["Gt(dB)"]
                var Gr = res.data[a]["Gr(dB)"]
                var NF = res.data[a]["NF(dB)"]
                var TLL = res.data[a]["TLL(dB)"]


                this.radarParams = [];
                var zwdataRadar = {}
                zwdataRadar.name = 'Pt';
                zwdataRadar.value = Pt;
                zwdataRadar.unit = 'kw';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'f';
                zwdataRadar.value = f;
                zwdataRadar.unit = 'Mhz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'PW';
                zwdataRadar.value = PW;
                zwdataRadar.unit = '1e-6*s';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'PRF';
                zwdataRadar.value = PRF;
                zwdataRadar.unit = 'pps';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Gt';
                zwdataRadar.value = Gt;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Gr';
                zwdataRadar.value = Gr;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'NF';
                zwdataRadar.value = NF;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'TLL';
                zwdataRadar.value = TLL;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}
              }

              //雷达参数2
              if (res.data[a]["num"] == 1) {
                var Lr = res.data[a]["Lr(dB)"]
                var Dop_Bw = res.data[a]["Dop Bw(Hz)"]
                var FA_Bw = res.data[a]["FA Bw(MHz)"]
                var Az_Bw = res.data[a]["Az Bw(deg)"]
                var Az_Rate = res.data[a]["Az Rate(deg/s)"]
                var Pd = res.data[a]["Pd"]
                var Pfa = res.data[a]["Pfa"]


                zwdataRadar.name = 'Lr';
                zwdataRadar.value = Lr;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Dop_Bw';
                zwdataRadar.value = Dop_Bw;
                zwdataRadar.unit = 'Hz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'FA_Bw';
                zwdataRadar.value = FA_Bw;
                zwdataRadar.unit = 'MHz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Az_Bw';
                zwdataRadar.value = Az_Bw;
                zwdataRadar.unit = 'deg';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Az_Rate';
                zwdataRadar.value = Az_Rate;
                zwdataRadar.unit = 'deg/s';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Pd';
                zwdataRadar.value = Pd;
                zwdataRadar.unit = '';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Pfa';
                zwdataRadar.value = Pfa;
                zwdataRadar.unit = '';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}
              }

              //大气以及目标参数
              if (res.data[a]["num"] == 2) {
                var RCS = res.data[a]["RCS"]
                var el_tgt_deg = res.data[a]["el_tgt_deg"]
                var target_length = res.data[a]["target_length"]
                var rain_fall = res.data[a]["rain_fall"]
                if (this.form.useType == 3) {
                  var T = res.data[a]["T"]
                }

                var tqParam = {}
                tqParam.name = '目标截面积';
                tqParam.value = RCS;
                tqParam.unit = '㎡';
                this.targetParams.push(tqParam)
                tqParam = {}

                tqParam.name = '目标高度';
                tqParam.value = el_tgt_deg;
                tqParam.unit = 'm';
                this.targetParams.push(tqParam)
                tqParam = {}

                tqParam.name = '目标长度';
                tqParam.value = target_length;
                tqParam.unit = 'm';
                this.targetParams.push(tqParam)
                tqParam = {}

                if (this.form.useType == 1) {
                  tqParam.name = '降雨率';
                } else if (this.form.useType == 2) {
                  tqParam.name = '降雪率';
                } else {
                  tqParam.name = '密度';
                }
                tqParam.value = rain_fall;
                if (this.form.useType == 3) {
                  tqParam.unit = 'g/m³';
                } else {
                  tqParam.unit = 'mm/h';
                }

                this.targetParams.push(tqParam)
                tqParam = {}

                if (this.form.useType == 3) {
                  tqParam.name = '温度'
                  tqParam.value = T;
                  tqParam.unit = '℃';
                  this.targetParams.push(tqParam)
                  tqParam = {}
                }
              }

              //无干扰情况下
              if (res.data[a]["num"] == 3) {

                for (let b = 0; b < res.data[a]["Swerling"].length; b++) {
                  let info = {};
                  info.case = res.data[a]["Swerling"][b];
                  if (b == 0) {
                    info.name = "Swerling Case ";
                  }

                  info.atmos = res.data[a]["DQSJ"][b].toFixed(6);
                  info.rain = res.data[a]["JYSJ"][b].toFixed(6);
                  info.range = res.data[a]["JCJL"][b].toFixed(6);
                  this.detectionRanges.push(info)
                }
              }

              //自卫干扰
              if (res.data[a]["num"] == 5) {
                //自卫干扰参数
                var zwdata = {}
                zwdata.name = '干扰功率';
                // console.log(res.data[a])
                // console.log(res.data[a]["SSJ_pwr_jam"])
                zwdata.value = res.data[a]["SSJ_pwr_jam"].toFixed(6);
                zwdata.unit = 'W';
                this.selfJammerData.push(zwdata)
                zwdata = {}

                zwdata.name = '干扰天线增益';
                zwdata.value = res.data[a]["SSJ_gain_dB"].toFixed(6);
                zwdata.unit = 'dB';
                this.selfJammerData.push(zwdata)
                zwdata = {}

                zwdata.name = '干扰带宽';
                zwdata.value = res.data[a]["SSJ_bw"].toFixed(6);
                zwdata.unit = 'MHz';
                this.selfJammerData.push(zwdata)
                zwdata = {}

                zwdata.name = '干扰损耗';
                zwdata.value = res.data[a]["SSJ_loss_dB"].toFixed(6);
                zwdata.unit = 'dB';
                this.selfJammerData.push(zwdata)
                zwdata = {}
              }

              //干扰机参数
              if (res.data[a]["num"] == 4) {

                this.jammerValues.push(res.data[a]["SOJ_pwr_jam"])
                this.jammerValues.push(res.data[a]["SOJ_gain_dB"])
                this.jammerValues.push(res.data[a]["SOJ_bw"])
                this.jammerValues.push(res.data[a]["jam_range"])
                this.jammerValues.push(res.data[a]["jam_height"])
                this.jammerValues.push(res.data[a]["SOJ_loss_dB"])
                this.jammerCount = res.data[a]["SOJ_pwr_jam"].length;
              }

              //干扰情况下的检测距离
              if (res.data[a]["num"] == 6) {


                for (let c = 0; c < res.data[a]["Swerling"].length; c++) {
                  let info = {};
                  info.case = res.data[a]["Swerling"][c];
                  info.atmos = res.data[a]["DQSJ"][c].toFixed(6);
                  info.rain = res.data[a]["JYSJ"][c].toFixed(6);
                  info.range = res.data[a]["GRJL"][c].toFixed(6);
                  this.jammedDetectionRanges.push(info)
                }
              }

            }
            var aaa = [];
            for (let a = 0; a < this.radarParams.length; a++) {
              if (a > 7) {

                this.radarParams1.push(this.radarParams[a])
              } else {
                aaa.push(this.radarParams[a])
              }

            }
            this.radarParams = aaa;
          }



          const combinedData = {
            ...dataFinal,
            jammedDetectionRanges: this.jammedDetectionRanges,
            detectionRanges: this.detectionRanges,
          };
          console.log(JSON.stringify(combinedData))
          this.dataFinal1.jsResult = JSON.stringify(combinedData);
          console.log("这是：" + this.chooseNum)
          this.showResultTable = true
          // this.saveImage()
        })
      }
      if (this.chooseNum == 1) {
        this.form.SOJ = 0
        this.form.SSJ = 1
        this.detectionRanges = []
        this.jammedDetectionRanges = []
        this.targetParams = []
        this.selfJammerData = []
        //自卫数据处理
        if (this.form.SOJ == 0) {
          // console.log('Form submitted:', this.$data);
          this.dataFinal = {
            "trans_pwr_radar": this.form.transmitterPower,
            "freq_radar": this.form.frequency,
            "pulse_width": this.form.pulseWidth,
            "GTDB_radar": this.form.transmitAntennaGain,
            "GRDB_radar": this.form.receiveAntennaGain,
            "GRDB_sl_radar": this.form.receiveAntennaSidelobe,
            "noise_fig_radar": this.form.noiseFigure,
            "loss_radar_dB": this.form.losses,
            "PRF": this.form.prf,

            "prob_det": this.form.probabilityOfDetection,
            "prob_false_alarm": this.form.probabilityOfFalseAlarm,
            "BW_dop": this.form.dopplerFilterBandwidth,
            "BW_fa": this.form.frequencyAgilityBandwidth,
            "Azimuth_bw": this.form.azimuthBeamwidth,
            "az_rate": this.form.azimuthScanRate,

            "RCS": this.form.rcs,
            "el_tgt_deg": this.form.elevationOfTarget,
            "target_length": this.form.lengthOfTarget,
            "rain_fall": this.form.rainFallRate,
            "T": this.form.T,
            "useType": this.form.useType,

            "SOJ": this.form.SOJ,
            "SSJ": this.form.SSJ,
            "num_jams": this.form.num_jams,

            //自卫干扰
            "SSJ_pwr_jam": this.form.SSJ_pwr_jam,
            "SSJ_gain_dB": this.form.SSJ_gain_dB,
            "SSJ_bw": this.form.SSJ_bw,
            "SSJ_loss_dB": this.form.SSJ_loss_dB,

            //远距离干扰
            "SOJ_pwr_jam": this.form.SOJ_pwr_jam,
            "SOJ_gain_dB": this.form.SOJ_gain_dB,
            "SOJ_bw": this.form.SOJ_bw,
            "jam_range": this.form.jam_range,
            "jam_height": this.form.jam_height,
            "SOJ_loss_dB": this.form.SOJ_loss_dB,
          }

          this.form1 = this.dataFinal;
          this.$axios({
            // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
            url: "http://127.0.0.1:9080/dqjy",//请求的后台接口
            method: "post",//get请求方式
            data: this.dataFinal,
            headers: {
              'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
              'Access-Control-Request-Method': 'POST',
              'Access-Control-Request-Headers': 'content-type',
            },
          }).then((res) => {
            console.log(res)
            if (res.data != undefined) {
              //循环
              for (let a = 0; a < res.data.length; a++) {
                if (res.data[a]["num"] == 0) {
                  //雷达参数1
                  var Pt = res.data[a]["Pt(kw)"]
                  var f = res.data[a]["f(Mhz)"]
                  var PW = res.data[a]["PW(1e-6*s)"]
                  var PRF = res.data[a]["PRF(pps)"]
                  var Gt = res.data[a]["Gt(dB)"]
                  var Gr = res.data[a]["Gr(dB)"]
                  var NF = res.data[a]["NF(dB)"]
                  var TLL = res.data[a]["TLL(dB)"]


                  this.radarParams = [];
                  var zwdataRadar = {}
                  zwdataRadar.name = 'Pt';
                  zwdataRadar.value = Pt;
                  zwdataRadar.unit = 'kw';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'f';
                  zwdataRadar.value = f;
                  zwdataRadar.unit = 'Mhz';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'PW';
                  zwdataRadar.value = PW;
                  zwdataRadar.unit = '1e-6*s';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'PRF';
                  zwdataRadar.value = PRF;
                  zwdataRadar.unit = 'pps';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'PRF';
                  zwdataRadar.value = PRF;
                  zwdataRadar.unit = 'pps';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'Gt';
                  zwdataRadar.value = Gt;
                  zwdataRadar.unit = 'dB';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'Gr';
                  zwdataRadar.value = Gr;
                  zwdataRadar.unit = 'dB';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'NF';
                  zwdataRadar.value = NF;
                  zwdataRadar.unit = 'dB';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'TLL';
                  zwdataRadar.value = TLL;
                  zwdataRadar.unit = 'dB';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}
                }

                //雷达参数2
                if (res.data[a]["num"] == 1) {
                  var Lr = res.data[a]["Lr(dB)"]
                  var Dop_Bw = res.data[a]["Dop Bw(Hz)"]
                  var FA_Bw = res.data[a]["FA Bw(MHz)"]
                  var Az_Bw = res.data[a]["Az Bw(deg)"]
                  var Az_Rate = res.data[a]["Az Rate(deg/s)"]
                  var Pd = res.data[a]["Pd"]
                  var Pfa = res.data[a]["Pfa"]


                  zwdataRadar.name = 'Lr';
                  zwdataRadar.value = Lr;
                  zwdataRadar.unit = 'dB';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'Dop_Bw';
                  zwdataRadar.value = Dop_Bw;
                  zwdataRadar.unit = 'Hz';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'FA_Bw';
                  zwdataRadar.value = FA_Bw;
                  zwdataRadar.unit = 'MHz';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'Az_Bw';
                  zwdataRadar.value = Az_Bw;
                  zwdataRadar.unit = 'deg';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'Az_Rate';
                  zwdataRadar.value = Az_Rate;
                  zwdataRadar.unit = 'deg/s';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'Pd';
                  zwdataRadar.value = Pd;
                  zwdataRadar.unit = '';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}

                  zwdataRadar.name = 'Pfa';
                  zwdataRadar.value = Pfa;
                  zwdataRadar.unit = '';
                  this.radarParams.push(zwdataRadar)
                  zwdataRadar = {}
                }

                //大气以及目标参数
                if (res.data[a]["num"] == 2) {
                  var RCS = res.data[a]["RCS"]
                  var el_tgt_deg = res.data[a]["el_tgt_deg"]
                  var target_length = res.data[a]["target_length"]
                  var rain_fall = res.data[a]["rain_fall"]
                  if (this.form.useType == 3) {
                    var T = res.data[a]["T"]
                  }

                  var tqParam = {}
                  tqParam.name = '目标截面积';
                  tqParam.value = RCS;
                  tqParam.unit = '㎡';
                  this.targetParams.push(tqParam)
                  tqParam = {}

                  tqParam.name = '目标高度';
                  tqParam.value = el_tgt_deg;
                  tqParam.unit = 'm';
                  this.targetParams.push(tqParam)
                  tqParam = {}

                  tqParam.name = '目标长度';
                  tqParam.value = target_length;
                  tqParam.unit = 'm';
                  this.targetParams.push(tqParam)
                  tqParam = {}

                  if (this.form.useType == 1) {
                    tqParam.name = '降雨率';
                  } else if (this.form.useType == 2) {
                    tqParam.name = '降雪率';
                  } else {
                    tqParam.name = '密度';
                  }
                  tqParam.value = rain_fall;
                  if (this.form.useType == 3) {
                    tqParam.unit = 'g/m³';
                  } else {
                    tqParam.unit = 'mm/h';
                  }
                  this.targetParams.push(tqParam)
                  tqParam = {}

                  if (this.form.useType == 3) {
                    tqParam.name = '温度'
                    tqParam.value = T;
                    tqParam.unit = '℃';
                    this.targetParams.push(tqParam)
                    tqParam = {}
                  }
                }

                //无干扰情况下
                //无干扰情况下
                if (res.data[a]["num"] == 3) {

                  for (let b = 0; b < res.data[a]["Swerling"].length; b++) {
                    let info = {};

                    info.case = res.data[a]["Swerling"][b];
                    info.atmos = res.data[a]["DQSJ"][b].toFixed(6);
                    info.rain = res.data[a]["JYSJ"][b].toFixed(6);
                    info.range = res.data[a]["JCJL"][b].toFixed(6);
                    this.detectionRanges.push(info)
                  }
                }
                //自卫干扰
                if (res.data[a]["num"] == 5) {
                  //自卫干扰参数
                  var zwdata = {}
                  zwdata.name = '干扰功率';
                  // console.log(res.data[a])
                  // console.log(res.data[a]["SSJ_pwr_jam"])
                  zwdata.value = res.data[a]["SSJ_pwr_jam"].toFixed(6);
                  zwdata.unit = 'W';
                  this.selfJammerData.push(zwdata)
                  zwdata = {}

                  zwdata.name = '干扰天线增益';
                  zwdata.value = res.data[a]["SSJ_gain_dB"].toFixed(6);
                  zwdata.unit = 'dB';
                  this.selfJammerData.push(zwdata)
                  zwdata = {}

                  zwdata.name = '干扰带宽';
                  zwdata.value = res.data[a]["SSJ_bw"].toFixed(6);
                  zwdata.unit = 'MHz';
                  this.selfJammerData.push(zwdata)
                  zwdata = {}

                  zwdata.name = '干扰损耗';
                  zwdata.value = res.data[a]["SSJ_loss_dB"].toFixed(6);
                  zwdata.unit = 'dB';
                  this.selfJammerData.push(zwdata)
                  zwdata = {}
                }

                //干扰机参数
                if (res.data[a]["num"] == 4) {

                  this.jammerValues.push(res.data[a]["SOJ_pwr_jam"])
                  this.jammerValues.push(res.data[a]["SOJ_gain_dB"])
                  this.jammerValues.push(res.data[a]["SOJ_bw"])
                  this.jammerValues.push(res.data[a]["jam_range"])
                  this.jammerValues.push(res.data[a]["jam_height"])
                  this.jammerValues.push(res.data[a]["SOJ_loss_dB"])
                  this.jammerCount = res.data[a]["SOJ_pwr_jam"].length;
                }

                //干扰情况下的检测距离
                if (res.data[a]["num"] == 6) {
                  for (let c = 0; c < res.data[a]["Swerling"].length; c++) {
                    let info = {};
                    info.case = res.data[a]["Swerling"][c];
                    info.atmos = res.data[a]["DQSJ"][c].toFixed(6);
                    info.rain = res.data[a]["JYSJ"][c].toFixed(6);
                    info.range = res.data[a]["GRJL"][c].toFixed(6);
                    this.jammedDetectionRanges.push(info)
                  }
                }



              }

              var aaa = [];
              for (let a = 0; a < this.radarParams.length; a++) {
                if (a > 7) {

                  this.radarParams1.push(this.radarParams[a])
                } else {
                  aaa.push(this.radarParams[a])
                }

              }
              this.radarParams = aaa;
            }

            const combinedData = {
              ...this.dataFinal,
              jammedDetectionRanges: this.jammedDetectionRanges,
              detectionRanges: this.detectionRanges,
            };
            console.log(JSON.stringify(combinedData))
            this.dataFinal1.jsResult = JSON.stringify(combinedData);
            this.$emit('dataFinal1', this.dataFinal1);
            this.showResultTable = true
          })
        }
      }
      if (this.chooseNum == 2) {
        this.form.SOJ = 0
        this.form.SSJ = 0
        this.detectionRanges = []
        this.jammedDetectionRanges = []
        this.targetParams = []
        //无干扰
        this.dataFinal = {
          "trans_pwr_radar": this.form.transmitterPower,
          "freq_radar": this.form.frequency,
          "pulse_width": this.form.pulseWidth,
          "GTDB_radar": this.form.transmitAntennaGain,
          "GRDB_radar": this.form.receiveAntennaGain,
          "GRDB_sl_radar": this.form.receiveAntennaSidelobe,
          "noise_fig_radar": this.form.noiseFigure,
          "loss_radar_dB": this.form.losses,
          "PRF": this.form.prf,

          "prob_det": this.form.probabilityOfDetection,
          "prob_false_alarm": this.form.probabilityOfFalseAlarm,
          "BW_dop": this.form.dopplerFilterBandwidth,
          "BW_fa": this.form.frequencyAgilityBandwidth,
          "Azimuth_bw": this.form.azimuthBeamwidth,
          "az_rate": this.form.azimuthScanRate,

          "RCS": this.form.rcs,
          "el_tgt_deg": this.form.elevationOfTarget,
          "target_length": this.form.lengthOfTarget,
          "rain_fall": this.form.rainFallRate,

          "SOJ": this.form.SOJ,
          "SSJ": this.form.SSJ,
          "num_jams": this.form.num_jams,
          "T": this.form.T,
          "useType": this.form.useType,

          //自卫干扰
          "SSJ_pwr_jam": this.form.SSJ_pwr_jam,
          "SSJ_gain_dB": this.form.SSJ_gain_dB,
          "SSJ_bw": this.form.SSJ_bw,
          "SSJ_loss_dB": this.form.SSJ_loss_dB,

          //远距离干扰
          "SOJ_pwr_jam": this.form.SOJ_pwr_jam,
          "SOJ_gain_dB": this.form.SOJ_gain_dB,
          "SOJ_bw": this.form.SOJ_bw,
          "jam_range": this.form.jam_range,
          "jam_height": this.form.jam_height,
          "SOJ_loss_dB": this.form.SOJ_loss_dB,


        }

        this.form1 = this.dataFinal;
        // console.log(this.dataFinal)

        this.$axios({
          url: "http://127.0.0.1:9080/dqjy",//请求的后台接口
          method: "post",//get请求方式
          data: this.dataFinal,
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'POST',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)
          if (res.data != undefined) {
            // console.log(res.data)
            //循环
            for (let a = 0; a < res.data.length; a++) {
              if (res.data[a]["num"] == 0) {
                //雷达参数1
                var Pt = res.data[a]["Pt(kw)"]
                var f = res.data[a]["f(Mhz)"]
                var PW = res.data[a]["PW(1e-6*s)"]
                var PRF = res.data[a]["PRF(pps)"]
                var Gt = res.data[a]["Gt(dB)"]
                var Gr = res.data[a]["Gr(dB)"]
                var NF = res.data[a]["NF(dB)"]
                var TLL = res.data[a]["TLL(dB)"]


                this.radarParams = [];
                var zwdataRadar = {}
                zwdataRadar.name = 'Pt';
                zwdataRadar.value = Pt;
                zwdataRadar.unit = 'kw';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'f';
                zwdataRadar.value = f;
                zwdataRadar.unit = 'Mhz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'PW';
                zwdataRadar.value = PW;
                zwdataRadar.unit = '1e-6*s';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'PRF';
                zwdataRadar.value = PRF;
                zwdataRadar.unit = 'pps';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'PRF';
                zwdataRadar.value = PRF;
                zwdataRadar.unit = 'pps';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Gt';
                zwdataRadar.value = Gt;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Gr';
                zwdataRadar.value = Gr;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'NF';
                zwdataRadar.value = NF;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'TLL';
                zwdataRadar.value = TLL;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}
              }

              //雷达参数2
              if (res.data[a]["num"] == 1) {
                var Lr = res.data[a]["Lr(dB)"]
                var Dop_Bw = res.data[a]["Dop Bw(Hz)"]
                var FA_Bw = res.data[a]["FA Bw(MHz)"]
                var Az_Bw = res.data[a]["Az Bw(deg)"]
                var Az_Rate = res.data[a]["Az Rate(deg/s)"]
                var Pd = res.data[a]["Pd"]
                var Pfa = res.data[a]["Pfa"]


                zwdataRadar.name = 'Lr';
                zwdataRadar.value = Lr;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Dop_Bw';
                zwdataRadar.value = Dop_Bw;
                zwdataRadar.unit = 'Hz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'FA_Bw';
                zwdataRadar.value = FA_Bw;
                zwdataRadar.unit = 'MHz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Az_Bw';
                zwdataRadar.value = Az_Bw;
                zwdataRadar.unit = 'deg';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Az_Rate';
                zwdataRadar.value = Az_Rate;
                zwdataRadar.unit = 'deg/s';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Pd';
                zwdataRadar.value = Pd;
                zwdataRadar.unit = '';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Pfa';
                zwdataRadar.value = Pfa;
                zwdataRadar.unit = '';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}
              }

              //大气以及目标参数
              if (res.data[a]["num"] == 2) {
                var RCS = res.data[a]["RCS"]
                var el_tgt_deg = res.data[a]["el_tgt_deg"]
                var target_length = res.data[a]["target_length"]
                var rain_fall = res.data[a]["rain_fall"]
                if (this.form.useType == 3) {
                  var T = res.data[a]["T"]
                }

                var tqParam = {}
                tqParam.name = '目标截面积';
                tqParam.value = RCS;
                tqParam.unit = '㎡';
                this.targetParams.push(tqParam)
                tqParam = {}

                tqParam.name = '目标高度';
                tqParam.value = el_tgt_deg;
                tqParam.unit = 'm';
                this.targetParams.push(tqParam)
                tqParam = {}

                tqParam.name = '目标长度';
                tqParam.value = target_length;
                tqParam.unit = 'm';
                this.targetParams.push(tqParam)
                tqParam = {}

                if (this.form.useType == 1) {
                  tqParam.name = '降雨率';
                } else if (this.form.useType == 2) {
                  tqParam.name = '降雪率';
                } else {
                  tqParam.name = '密度';
                }
                tqParam.value = rain_fall;
                if (this.form.useType == 3) {
                  tqParam.unit = 'g/m³';
                } else {
                  tqParam.unit = 'mm/h';
                }
                this.targetParams.push(tqParam)
                tqParam = {}

                if (this.form.useType == 3) {
                  tqParam.name = '温度'
                  tqParam.value = T;
                  tqParam.unit = '℃';
                  this.targetParams.push(tqParam)
                  tqParam = {}
                }
              }

              //无干扰情况下
              //无干扰情况下
              if (res.data[a]["num"] == 3) {

                for (let b = 0; b < res.data[a]["Swerling"].length; b++) {
                  let info = {};


                  info.case = res.data[a]["Swerling"][b];
                  info.atmos = res.data[a]["DQSJ"][b].toFixed(6);
                  info.rain = res.data[a]["JYSJ"][b].toFixed(6);
                  info.range = res.data[a]["JCJL"][b].toFixed(6);
                  this.detectionRanges.push(info)
                }
              }

            }
            var aaa = [];
            for (let a = 0; a < this.radarParams.length; a++) {
              if (a > 7) {

                this.radarParams1.push(this.radarParams[a])
              } else {
                aaa.push(this.radarParams[a])
              }

            }
            this.radarParams = aaa;
          }


          const combinedData = {
            ...this.dataFinal,
            detectionRanges: this.detectionRanges,
          };
          this.dataFinal1.jsResult = JSON.stringify(combinedData);
          this.showResultTable = true
          console.log(this.detectionRanges)
        })
      }
      if (this.chooseNum == 3) {
        this.form.SOJ = 1
        this.form.SSJ = 1
        this.form.SOJ_pwr_jam = []
        this.form.SOJ_gain_dB = []
        this.form.SOJ_bw = []
        this.form.jam_range = []
        this.form.jam_height = []
        this.form.SOJ_loss_dB = []
        this.detectionRanges = []
        this.jammedDetectionRanges = []
        this.targetParams = []
        this.selfJammerData = []
        for (let a = 0; a < this.tableData.length; a++) {
          this.form.SOJ_pwr_jam.push(this.tableData[a].Power)
          this.form.SOJ_gain_dB.push(this.tableData[a].Gain)
          this.form.SOJ_bw.push(this.tableData[a].Bandwidth)
          this.form.jam_range.push(this.tableData[a].Range)
          this.form.jam_height.push(this.tableData[a].Height)
          this.form.SOJ_loss_dB.push(this.tableData[a].Loss)
        }
        this.dataFinal = {
          "trans_pwr_radar": this.form.transmitterPower,
          "freq_radar": this.form.frequency,
          "pulse_width": this.form.pulseWidth,
          "GTDB_radar": this.form.transmitAntennaGain,
          "GRDB_radar": this.form.receiveAntennaGain,
          "GRDB_sl_radar": this.form.receiveAntennaSidelobe,
          "noise_fig_radar": this.form.noiseFigure,
          "loss_radar_dB": this.form.losses,
          "PRF": this.form.prf,

          "prob_det": this.form.probabilityOfDetection,
          "prob_false_alarm": this.form.probabilityOfFalseAlarm,
          "BW_dop": this.form.dopplerFilterBandwidth,
          "BW_fa": this.form.frequencyAgilityBandwidth,
          "Azimuth_bw": this.form.azimuthBeamwidth,
          "az_rate": this.form.azimuthScanRate,

          "RCS": this.form.rcs,
          "el_tgt_deg": this.form.elevationOfTarget,
          "target_length": this.form.lengthOfTarget,
          "rain_fall": this.form.rainFallRate,
          "T": this.form.T,
          "useType": this.form.useType,

          "SOJ": this.form.SOJ,
          "SSJ": this.form.SSJ,
          "num_jams": this.form.num_jams,

          //自卫干扰
          "SSJ_pwr_jam": this.form.SSJ_pwr_jam,
          "SSJ_gain_dB": this.form.SSJ_gain_dB,
          "SSJ_bw": this.form.SSJ_bw,
          "SSJ_loss_dB": this.form.SSJ_loss_dB,

          //远距离干扰
          "SOJ_pwr_jam": this.form.SOJ_pwr_jam,
          "SOJ_gain_dB": this.form.SOJ_gain_dB,
          "SOJ_bw": this.form.SOJ_bw,
          "jam_range": this.form.jam_range,
          "jam_height": this.form.jam_height,
          "SOJ_loss_dB": this.form.SOJ_loss_dB,
        }

        this.form1 = this.dataFinal;
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:9080/dqjy",//请求的后台接口
          method: "post",//get请求方式
          data: this.dataFinal,
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'POST',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)
          if (res.data != undefined) {
            //循环
            for (let a = 0; a < res.data.length; a++) {
              if (res.data[a]["num"] == 0) {
                //雷达参数1
                var Pt = res.data[a]["Pt(kw)"]
                var f = res.data[a]["f(Mhz)"]
                var PW = res.data[a]["PW(1e-6*s)"]
                var PRF = res.data[a]["PRF(pps)"]
                var Gt = res.data[a]["Gt(dB)"]
                var Gr = res.data[a]["Gr(dB)"]
                var NF = res.data[a]["NF(dB)"]
                var TLL = res.data[a]["TLL(dB)"]


                this.radarParams = [];
                var zwdataRadar = {}
                zwdataRadar.name = 'Pt';
                zwdataRadar.value = Pt;
                zwdataRadar.unit = 'kw';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'f';
                zwdataRadar.value = f;
                zwdataRadar.unit = 'Mhz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'PW';
                zwdataRadar.value = PW;
                zwdataRadar.unit = '1e-6*s';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'PRF';
                zwdataRadar.value = PRF;
                zwdataRadar.unit = 'pps';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'PRF';
                zwdataRadar.value = PRF;
                zwdataRadar.unit = 'pps';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Gt';
                zwdataRadar.value = Gt;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Gr';
                zwdataRadar.value = Gr;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'NF';
                zwdataRadar.value = NF;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'TLL';
                zwdataRadar.value = TLL;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}
              }

              //雷达参数2
              if (res.data[a]["num"] == 1) {
                var Lr = res.data[a]["Lr(dB)"]
                var Dop_Bw = res.data[a]["Dop Bw(Hz)"]
                var FA_Bw = res.data[a]["FA Bw(MHz)"]
                var Az_Bw = res.data[a]["Az Bw(deg)"]
                var Az_Rate = res.data[a]["Az Rate(deg/s)"]
                var Pd = res.data[a]["Pd"]
                var Pfa = res.data[a]["Pfa"]


                zwdataRadar.name = 'Lr';
                zwdataRadar.value = Lr;
                zwdataRadar.unit = 'dB';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Dop_Bw';
                zwdataRadar.value = Dop_Bw;
                zwdataRadar.unit = 'Hz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'FA_Bw';
                zwdataRadar.value = FA_Bw;
                zwdataRadar.unit = 'MHz';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Az_Bw';
                zwdataRadar.value = Az_Bw;
                zwdataRadar.unit = 'deg';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Az_Rate';
                zwdataRadar.value = Az_Rate;
                zwdataRadar.unit = 'deg/s';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Pd';
                zwdataRadar.value = Pd;
                zwdataRadar.unit = '';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}

                zwdataRadar.name = 'Pfa';
                zwdataRadar.value = Pfa;
                zwdataRadar.unit = '';
                this.radarParams.push(zwdataRadar)
                zwdataRadar = {}
              }


              //大气以及目标参数
              if (res.data[a]["num"] == 2) {
                var RCS = res.data[a]["RCS"]
                var el_tgt_deg = res.data[a]["el_tgt_deg"]
                var target_length = res.data[a]["target_length"]
                var rain_fall = res.data[a]["rain_fall"]
                if (this.form.useType == 3) {
                  var T = res.data[a]["T"]
                }

                var tqParam = {}
                tqParam.name = '目标截面积';
                tqParam.value = RCS;
                tqParam.unit = '㎡';
                this.targetParams.push(tqParam)
                tqParam = {}

                tqParam.name = '目标高度';
                tqParam.value = el_tgt_deg;
                tqParam.unit = 'm';
                this.targetParams.push(tqParam)
                tqParam = {}

                tqParam.name = '目标长度';
                tqParam.value = target_length;
                tqParam.unit = 'm';
                this.targetParams.push(tqParam)
                tqParam = {}

                if (this.form.useType == 1) {
                  tqParam.name = '降雨率';
                } else if (this.form.useType == 2) {
                  tqParam.name = '降雪率';
                } else {
                  tqParam.name = '密度';
                }
                tqParam.value = rain_fall;
                if (this.form.useType == 3) {
                  tqParam.unit = 'g/m³';
                } else {
                  tqParam.unit = 'mm/h';
                }
                this.targetParams.push(tqParam)
                tqParam = {}

                if (this.form.useType == 3) {
                  tqParam.name = '温度'
                  tqParam.value = T;
                  tqParam.unit = '℃';
                  this.targetParams.push(tqParam)
                  tqParam = {}
                }
              }

              //无干扰情况下
              if (res.data[a]["num"] == 3) {

                for (let b = 0; b < res.data[a]["Swerling"].length; b++) {
                  let info = {};

                  info.case = res.data[a]["Swerling"][b];
                  info.atmos = res.data[a]["DQSJ"][b].toFixed(6);
                  info.rain = res.data[a]["JYSJ"][b].toFixed(6);
                  info.range = res.data[a]["JCJL"][b].toFixed(6);
                  this.detectionRanges.push(info)
                }
              }

              //自卫干扰
              if (res.data[a]["num"] == 5) {
                //自卫干扰参数
                var zwdata = {}
                zwdata.name = '干扰功率';
                // console.log(res.data[a])
                // console.log(res.data[a]["SSJ_pwr_jam"])
                zwdata.value = res.data[a]["SSJ_pwr_jam"].toFixed(6);
                zwdata.unit = 'W';
                this.selfJammerData.push(zwdata)
                zwdata = {}

                zwdata.name = '干扰天线增益';
                zwdata.value = res.data[a]["SSJ_gain_dB"].toFixed(6);
                zwdata.unit = 'dB';
                this.selfJammerData.push(zwdata)
                zwdata = {}

                zwdata.name = '干扰带宽';
                zwdata.value = res.data[a]["SSJ_bw"].toFixed(6);
                zwdata.unit = 'MHz';
                this.selfJammerData.push(zwdata)
                zwdata = {}

                zwdata.name = '干扰损耗';
                zwdata.value = res.data[a]["SSJ_loss_dB"].toFixed(6);
                zwdata.unit = 'dB';
                this.selfJammerData.push(zwdata)
                zwdata = {}
              }

              //干扰机参数
              if (res.data[a]["num"] == 4) {

                this.jammerValues.push(res.data[a]["SOJ_pwr_jam"])
                this.jammerValues.push(res.data[a]["SOJ_gain_dB"])
                this.jammerValues.push(res.data[a]["SOJ_bw"])
                this.jammerValues.push(res.data[a]["jam_range"])
                this.jammerValues.push(res.data[a]["jam_height"])
                this.jammerValues.push(res.data[a]["SOJ_loss_dB"])
                this.jammerCount = res.data[a]["SOJ_pwr_jam"].length;
              }

              //干扰情况下的检测距离
              if (res.data[a]["num"] == 6) {


                for (let c = 0; c < res.data[a]["Swerling"].length; c++) {
                  let info = {};
                  info.case = res.data[a]["Swerling"][c];
                  info.atmos = res.data[a]["DQSJ"][c].toFixed(6);
                  info.rain = res.data[a]["JYSJ"][c].toFixed(6);
                  info.range = res.data[a]["GRJL"][c].toFixed(6);
                  this.jammedDetectionRanges.push(info)
                }
              }

            }

            var aaa = [];
            for (let a = 0; a < this.radarParams.length; a++) {
              if (a > 7) {

                this.radarParams1.push(this.radarParams[a])
              } else {
                aaa.push(this.radarParams[a])
              }

            }
            this.radarParams = aaa;
          }

          const combinedData = {
            ...this.dataFinal,
            jammedDetectionRanges: this.jammedDetectionRanges,
            detectionRanges: this.detectionRanges,
          };
          this.dataFinal1.jsResult = JSON.stringify(combinedData);

          this.showResultTable = true


        })
      }


    },
    async saveImage() {
      await this.$nextTick();
      const targetDiv = document.getElementById('capture');

      // 1. 克隆并保护关键内容
      const clone = targetDiv.cloneNode(true);
      clone.style.position = 'absolute';
      clone.style.left = '-9999px';
      clone.style.whiteSpace = 'pre-wrap';
      clone.style.fontFamily = 'Arial, sans-serif';
      clone.style.fontSize = '1vw';

      //   // 3. 处理内部元素的overflow（如果有嵌套滚动区域）
      const scrollableElements = clone.querySelectorAll('*[style*="overflow"]');
      scrollableElements.forEach(el => {
        el.style.overflow = 'visible';
        el.style.height = 'auto';
      });

      // 2. 保护特殊单位

      // 3. 处理对齐文本
      const lines = clone.innerHTML.split('<br>');
      if (lines.length > 1) {
        clone.innerHTML = lines.map(line => `
      <div style="display: flex; margin: 2px 0;">
        <div style="min-width: 100px;">${line}</div>
        <div>${line.split(':')[1] || ''}</div>
      </div>
    `).join('');
      }

      document.body.appendChild(clone);
      await new Promise(resolve => setTimeout(resolve, 500));

      // 4. 截图
      const canvas = await html2canvas(clone, {
        width: clone.scrollWidth,
        height: clone.scrollHeight,
        scale: 2,
        letterRendering: true,
        useCORS: true,
        backgroundColor: 'rgba(49,73,163,0.94)'
      });
      var imageData = canvas.toDataURL('image/png')

      console.log(imageData)

      // this.$emit('capture', canvas.toDataURL('image/png'));
      var dataa = this.handleCapture(imageData)
      console.log(dataa)
      document.body.removeChild(clone);
    },
    save() {
      this.saveImage();

      console.log(this.dataFinal1)

    },
    dataURLtoBlob(dataURL) {
      const arr = dataURL.split(',');
      const mime = arr[0].match(/:(.*?);/)[1];
      const bstr = atob(arr[1]);
      let n = bstr.length;
      const u8arr = new Uint8Array(n);

      while (n--) {
        u8arr[n] = bstr.charCodeAt(n);
      }

      return new Blob([u8arr], { type: mime });
    },
    handleCapture(dataURL) {

      const blob = this.dataURLtoBlob(dataURL);
      // 3. 创建FormData并添加文件
      const formData = new FormData();
      formData.append('file', blob, 'screenshot.png');
      formData.append('additionalData', '任何其他表单数据');

      // 4. 上传到服务器
      fileUpdate(blob).then((res) => {
        console.log(res.data.url);
        this.dataFinal1.allImg = res.data.url;
        saveJsResult(this.dataFinal1).then((res) => {
          console.log(res);
        })
      })



    },
    getInfo() {
      this.dataFinal1.jsId = this.$route.query.id;
    },
    dataInitialize() {
      console.log(this.form1)
      this.form.transmitterPower = this.form1.trans_pwr_radar;
      this.form.frequency = this.form1.freq_radar;
      this.form.pulseWidth = this.form1.pulse_width;
      this.form.transmitAntennaGain = this.form1.az_rate;
      this.form.receiveAntennaGain = this.form1.GRDB_radar;
      this.form.receiveAntennaSidelobe = this.form1.GRDB_sl_radar;
      this.form.noiseFigure = this.form1.noise_fig_radar;
      this.form.losses = this.form1.loss_radar_dB;
      this.form.prf = this.form1.PRF;
      this.form.probabilityOfDetection = this.form1.prob_det;
      this.form.probabilityOfFalseAlarm = this.form1.prob_false_alarm;
      this.form.dopplerFilterBandwidth = this.form1.BW_dop;
      this.form.frequencyAgilityBandwidth = this.form1.BW_fa;
      this.form.azimuthBeamwidth = this.form1.Azimuth_bw;
      this.form.azimuthScanRate = this.form1.az_rate;
      this.form.rcs = this.form1.RCS;
      this.form.elevationOfTarget = this.form1.el_tgt_deg;
      this.form.lengthOfTarget = this.form1.target_length;
      this.form.useType = this.form1.useType;
      this.form.rainFallRate = this.form1.rain_fall;
      this.form.T = this.form1.T;
      this.form.jammingType = this.chooseNum;
      this.form.SOJ = this.form1.SOJ;
      this.form.SSJ = this.form1.SSJ;
      this.form.SSJ_pwr_jam = this.form1.SSJ_pwr_jam;
      this.form.SSJ_gain_dB = this.form1.SSJ_gain_dB;
      this.form.SSJ_bw = this.form1.SSJ_bw;
      this.form.SSJ_loss_dB = this.form1.SSJ_loss_dB;
      this.form.num_jams = this.form1.num_jams;
      this.form.yjlList = [];
      this.form.SOJ_pwr_jam = this.form1.SOJ_pwr_jam;
      this.form.SOJ_gain_dB = this.form1.SOJ_gain_dB;
      this.form.SOJ_bw = this.form1.SOJ_bw;
      this.form.jam_range = this.form1.jam_range;
      this.form.jam_height = this.form1.jam_height;
      this.form.SOJ_loss_dB = this.form1.SOJ_loss_dB;
    },
    clear() {
      this.form.transmitterPower = 0;
      this.form.frequency = 0;
      this.form.pulseWidth = 0;
      this.form.transmitAntennaGain = 0;
      this.form.receiveAntennaGain = 0;
      this.form.receiveAntennaSidelobe = 0;
      this.form.noiseFigure = 0;
      this.form.losses = 0;
      this.form.prf = 0;

      this.form.probabilityOfDetection = 0;
      this.form.probabilityOfFalseAlarm = 0;
      this.form.dopplerFilterBandwidth = 0;
      this.form.frequencyAgilityBandwidth = 0;
      this.form.azimuthBeamwidth = 0;
      this.form.azimuthScanRate = 0;


      this.form.rcs = 0;
      this.form.elevationOfTarget = 0;
      this.form.lengthOfTarget = 0;
      this.form.rainFallRate = 0;

      this.form.SOJ = undefined;
      this.form.SSJ = undefined;
      this.form.jammingType = 2;
      this.form.useType = 0;
      this.form.T = 0;


      //自卫干扰参数
      this.form.SSJ_pwr_jam = 0;
      this.form.SSJ_gain_dB = 0;
      this.form.SSJ_bw = 0;
      this.form.SSJ_loss_dB = 0;


      //远距离干扰
      this.form.num_jams = 0;


      //远距离干扰机参数
      this.form.Power = 0;
      this.form.Gain = 0;
      this.form.Bandwidth = 0;
      this.form.Range = 0;
      this.form.Height = 0;
      this.form.Loss = 0;


      //远距离参数数组
      this.form.yjlList = [];


      this.form.SOJ_pwr_jam = [];
      this.form.SOJ_gain_dB = [];
      this.form.SOJ_bw = [];
      this.form.jam_range = [];
      this.form.jam_height = [];
      this.form.SOJ_loss_dB = [];
      this.showResultTable = false;
    },
  },
  mounted() {
    this.getInfo();
  }
};
</script>

<style scoped>
.edit-controls .el-button {
  margin-left: 1vw;
}


.radar-result h3 {
  margin: 3vw 0 1vw 0;
  color: #7cdeff;
  font-size: 1.2vw;
  border-bottom: 1px solid rgba(124, 222, 255, 0.3);
  padding-bottom: 5px;
}

.content-container {
  padding-left: 1vw;
  width: 100%;
  height: 100%;

  /* overflow-y: auto; */
  /* 添加垂直滚动条 */
}


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

.inputBox {
  height: 100%;
  width: 98%;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  align-content: space-around;
}

.box1 {
  width: 48%;
  height: 46%;
  background-image: url("@/assets/img/dqjsBox1.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;



}

.queding {
  height: 1.5vw;
  width: 4vw;
  background-image: url("@/assets/img/queding.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  font-size: 0.8vw;
  line-height: 1.5vw;
  border-radius: 1vw;
  text-align: center;
  color: #FFFFFF;
  margin-left: 88%;
}

.hg {
  width: 94%;
  margin: 0 auto;
  margin-top: 3%;
  height: 5vh;
  background-image: url("@/assets/img/hg.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  display: flex;
  justify-content: space-between;


}

.smallTitle {
  width: 24%;
  height: 100%;
  display: flex;
  align-items: center;
  margin-left: 3%;

}

.baiquan {
  height: 30%;
  width: 15%;
  background-color: #FFFFFF;
  border-radius: 0.5vw;
  margin-right: 5%;
}

.baititle {
  font-size: 1vw;
  color: #FFFFFF;
}

.sx {
  width: 8%;
  height: 100%;
  display: flex;
  align-items: center;
  margin-right: 2%;
  justify-content: space-around;
}

.sxFont {
  color: #FFFFFF;
  font-size: 0.7vw;
}

.password-input-container {
  width: 45%;
  height: 90%;
  position: absolute;
  top: 8%;
  right: 1%;
}

.boxSr1 {
  width: 90%;
  margin: 0 auto;
  height: 78%;
  margin-top: 1%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.boxSr2 {
  width: 100%;
  margin: 0 auto;
  height: 15vh;
  /*background-color: pink;*/
  margin-top: 1%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.twoInput {
  width: 100%;
  height: 13%;
  display: flex;
  justify-content: space-between;
  justify-items: center;
}

.leftInput {
  width: 48%;
  display: flex;
  align-items: center;
  position: relative;
}

.rightInput {
  width: 48%;
  display: flex;
  align-items: center;
  position: relative;
}

.leftTitle {
  width: 65%;
  color: #FFFFFF;
  font-size: 0.9vw;
}

.rightTitle {
  width: 65%;
  color: #FFFFFF;
  font-size: 0.9vw;
}

input {
  width: 90%;
  height: 100%;
  border: none;
  outline: none;
  color: white;
  font-size: 0.9vw;
  /* 文字颜色 */
  /* background-color: transparent;*/
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

.oneInput {
  width: 90%;
  height: 13%;
  display: flex;
  justify-content: center;
  justify-items: center;
  position: relative;
}

.oneLeftTitle {

  color: #FFFFFF;
  margin-right: 1%;
  width: 60%;
  text-align: right;
  font-size: 0.8vw;

}

.password-input-container1 {
  position: relative;
  width: 20%;
  height: 90%;
  margin-right: 2.5%;


}

.radio-group {
  width: 60%;
  height: 100%;
  margin: 0 auto;
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
}

.radioList {
  height: 10%;
  width: 90%;
  margin: 0 auto;
  margin-top: 2.5%;
  position: relative;
}

.boxSr3 {
  width: 100%;
  margin: 0 auto;
  height: 11vh;
  /*background-color: pink;*/
  margin-top: 1%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.oneInput3 {
  width: 85%;
  height: 4.5vh;
  display: flex;
  justify-content: center;
  justify-items: center;
  position: relative;
}


.radio-group1 {
  width: 100%;
  height: 100%;
  margin: 0 auto;
  display: flex;
  justify-content: space-around;
  align-content: center;
  align-items: center;

}

.radio-option1 {
  display: flex;
  align-items: center;
  cursor: pointer;

}

.radio-input1 {
  appearance: none;
  width: 0.75vw;
  height: 0.75vw;
  border: 2px solid #23f9fd;
  border-radius: 50%;
  margin-right: 0.5vw;
  position: relative;
  cursor: pointer;
  transition: all 0.2s;
}

.radio-input1:checked {
  border: none;
}

.radio-input1:checked::after {
  content: '';
  position: absolute;
  width: 0.75vw;
  height: 0.75vw;


  background: #23f9fd;
  border-radius: 50%;
}

.radio-label1 {
  font-size: 0.75vw;
  color: #FFFFFF;
}

.radioList1 {
  height: 10%;
  width: 90%;
  margin: 0 auto;
  margin-top: 2.5%;
  position: relative;
}

.ylgr {
  width: 100%;
}


.smallJian {
  width: 92%;
  height: 1.5vw;
  margin: 0 auto;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  margin-top: 1.5%;
}

.smallJianFont {
  width: 20%;
  height: 1.5vw;
  line-height: 1.5vw;
  font-size: 0.9vw;
  margin-left: 1.5%;
  color: #FFFFFF;
}

.yjlsl {
  width: 92%;
  height: 1.5vw;

  margin: 0 auto;
  position: relative;
  display: flex;
  justify-content: flex-start;
  margin-top: 2%;
}

.grsl {
  width: 15%;
  color: #FFFFFF;
  font-size: 0.9vw;
}

.password-input-containergr {
  width: 8%;
  height: 100%;
  position: absolute;
  left: 12%;

}

.grsj {
  margin-top: 1vw;
  margin-bottom: 2vw;
}

.tableInputOne {
  width: 96%;
  height: 100%;
  margin: 0 auto;
  font-size: 0.8vw;
  border-collapse: collapse;
}

.tableInputOne input {
  width: 80%;
  height: 50%;
  outline: none;
  color: white;
  /* 文字颜色 */
  background-color: rgba(0, 148, 255, 0.38);
  margin-left: 8%;
  margin-top: 1vw;
  border-radius: 2vw;

}


.zwgr {
  width: 100%;
}

.zwgrcs {
  width: 90%;
  height: 10vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  margin-bottom: 2vw;


}

.oneInputzw {
  width: 85%;
  height: 16%;
  display: flex;
  justify-content: center;
  justify-items: center;
  position: relative;
  align-items: center;
}


.box1::-webkit-scrollbar {
  width: 0.5vw;
  /* 垂直滚动条宽度 */
  height: 0.5vw;
  /* 水平滚动条高度 */
}

.box1::-webkit-scrollbar-track {
  background: transparent;
  /* 轨道颜色 */
}

.box1::-webkit-scrollbar-thumb {
  background: rgba(51, 216, 255);
  /* 滑块悬停颜色 */
  border-radius: 0.5vw;
  /* 滑块圆角 */
}

.box1::-webkit-scrollbar-thumb:hover {
  background: rgba(51, 216, 255);
  /* 滑块悬停颜色 */
}

.resultBox {
  height: 100%;
  width: 98%;
  margin-top: 2vh;

}

.resultInput {
  height: 40%;
  width: 100%;
}

.resultJianTop {
  width: 16%;
  height: 12%;
  position: relative;
  display: flex;
  align-items: center;
}

.resultName {
  position: absolute;
  z-index: 101;
  background-color: transparent;
  text-align: center;
  color: #FFFFFF;
  font-size: 1vw;
  width: 80%;
  line-height: 2vw;
}

.resultLdList {

  width: 100%;
  height: 78%;
  margin-top: 1%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;

}

.oneLine {

  width: 100%;
  height: 40%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

.resultSmallBox {
  background-image: url("../../assets/img/ldresult.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  height: 90%;
  width: 10%;
  display: flex;
  flex-direction: column;
}

.smallTop {
  width: 100%;
  height: 50%;

  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.smallIconInfo {
  width: 13%;
  height: 20%;
  border-radius: 1vw;
  background-color: #1fe5ff;
  margin-right: 3%;


}

.smallIconFont {
  color: #1fe5ff;
  font-size: 1vw;
  justify-content: flex-start;
}

.smallDown {
  width: 100%;
  height: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.1vw;
}


.resultInput1 {
  height: 25%;
  width: 100%;
}

.resultJianTop1 {
  width: 20.75%;
  height: 19.2%;
  position: relative;
  display: flex;
  align-items: center;
}

.resultHjList {
  width: 98%;
  height: 50%;
  margin: 0 auto;
  margin-top: 2%;
  justify-content: space-between;
  display: flex;
  flex-direction: row;

}

.HjInfo {
  height: 100%;
  width: 16%;
  background-image: url("../../assets/img/HjBg.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column;
  padding: 0 1.3%;
}

.HjInfo1 {
  height: 100%;
  width: 13%;
  background-image: url("../../assets/img/HjBg.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column;
  padding: 0 1.3%;
}

.HjTop {

  height: 45%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  font-size: 0.9vw;
  color: #FFFFFF;
}

.HjDown {
  height: 55%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  color: #1fe5ff;


}

.resultInput2 {
  height: 30vh;
  width: 100%;
  margin-top: 2vh;
}

.resultJianTop2 {
  width: 27.25%;
  height: 12%;
  position: relative;
  display: flex;
  align-items: center;
}

.resultTabl1 {
  width: 98%;
  height: 80%;
  margin: 0 auto;
  margin-top: 1.5%;
  background-image: url("../../assets/img/resultTable.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  position: relative;
}

.tableOne {
  width: 86%;
  font-family: Arial, sans-serif;
  height: 80%;
  border-collapse: collapse;
  position: absolute;
  top: 10%;
  left: 7%;
  font-size: 0.8vw;
  color: #FFFFFF;

}


.tableOne th,
.tableOne td {
  text-align: center;

}

.case-header {
  color: white;
  height: 2.5vw;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.9vw;
}


.tableOne tbody tr td:first-child {
  text-align: center;
  font-weight: bold;
  color: #FFFFFF;
}

.tableL1 {
  height: 80%;
  background-color: rgba(0, 148, 255, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 2vw;
  color: #FFFFFF;
  margin-top: 1vw;
}

.first-header {
  border-top-left-radius: 2vw;
  border-bottom-left-radius: 2vw;
}

.last-header {

  border-top-right-radius: 2vw;
  border-bottom-right-radius: 2vw;
}

.theaderInfo {
  background-color: rgba(0, 148, 255, 0.6);
}

.infoList1 {
  padding-top: 1vw;
  display: flex;
  align-items: center;
  justify-content: center;
}


.resultInput3 {
  height: 70%;
  width: 100%;
  margin-top: 2%;
}

.resultJianTop3 {
  width: 30%;
  height: 6%;
  position: relative;
  display: flex;
  align-items: center;
}

.resultTabl3 {
  width: 98%;
  height: 85%;
  margin: 0 auto;
  margin-top: 1.5%;
  background-image: url("../../assets/img/resultTable.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  position: relative;
}


.resultInput4 {
  height: 25%;
  width: 100%;
}

.resultJianTop4 {
  width: 20.75%;
  height: 19.2%;
  position: relative;
  display: flex;
  align-items: center;
}

.baocun {
  height: 1.5vw;
  width: 4vw;
  background-image: url("@/assets/img/queding.png");
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  font-size: 0.8vw;
  position: absolute;
  line-height: 1.5vw;
  border-radius: 1vw;
  text-align: center;
  color: #FFFFFF;
  right: 2vw;
}

.button1 {
  border-radius: 2vw;
  line-height: 0vh;
  background-image: url('@/assets/img/baocun.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  margin-left: 1vw;
}

.waibiankuang {
  background-image: url('@/assets/img/wbk.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  padding-top: 2vh;
  padding-left: 1vw;
  overflow-y: scroll;
}

.waibiankuang::-webkit-scrollbar {
  display: none;
  /* Chrome, Safari, Edge */
}
</style>
