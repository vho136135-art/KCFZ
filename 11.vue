r:<template>
  <div class="background-container">
    <div class="content-container">
      <div
        style="display: flex;width: 96%;margin-bottom: 1.5vh;margin-top: 1.5vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color:#196EC1; font-size: 1.6vw;font-weight: 500;">
          声呐探测距离估算
        </div>
        <!--        <el-button class="button1" style="height: 1.5vw;margin-left: 33vw;" @click="save">保存</el-button>-->
      </div>
      <div style="display: flex;width: 96.5%;height: 87%;flex-direction: column;" class="waibiankuang">
        <div slot="foot" class="dialog-footer">
          <el-button class="button2" @click="test">载入测试值</el-button>
          <el-button class="button2" @click="clear">清除</el-button>
          <el-button class="button2" @click="save">保存</el-button>
          <el-button class="button3" @click="sumbitInfo">计算</el-button>
        </div>
        <div style="display: flex;">
          <!-- <div class="back" style="margin-right: 2vw;">
            <div class="biaotou">
              <div class="biaotou-left">声纳方程式计算器</div>
            </div>
            <div class="formaction">
              计算类型
              <div style="width: 5vw;text-align: left;color: #fff;" @click="showOptions" @focus="onFocus" @blur="onBlur"
                tabindex="0">
                <div class="xialakuang">
                  <div class="selected-option">
                    {{ this.calculationType || '' }}
                  </div>
                  <img :src="require('@/assets/img/graphDown.png')"
                    style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                    v-if="typePic1 == 0">
                  <img :src="require('@/assets/img/graphUp.png')"
                    style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                    v-if="typePic1 == 1">
                </div>
              </div>
              <ul v-if="showOption" class="options">
                <li v-for="(item, index) in calculationTypeList" :key="index" @click="selectOption(item)">
                  {{ item.label }}
                </li>
              </ul>
            </div>
          </div> -->
          <div style="display: flex;flex-wrap: wrap;  margin: 0 auto; width: 70vw;">
            <div class="back" style="margin-right: 2vw;">
              <div class="biaotou">
                <div class="biaotou-left">声呐参数</div>
              </div>
              <div class="formaction">
                模型
                <div style="width: 5vw;text-align: left;color: #fff;" @click="showOptions1" @focus="onFocus"
                  @blur="onBlur" tabindex="0">
                  <div class="xialakuang">
                    <!--                  <img :src="require('@/assets/img/graphInput.png')"-->
                    <!--                    style="position: absolute;z-index: 99;width:33%;height: 80%;">-->
                    <div class="selected-option">
                      {{ this.Mode || '' }}
                    </div>
                    <img :src="require('@/assets/img/graphDown.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                      v-if="typePic2 == 0">
                    <img :src="require('@/assets/img/graphUp.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                      v-if="typePic2 == 1">
                  </div>
                </div>
                <ul v-if="showOption1" class="options">
                  <li v-for="(item, index) in ModeList" :key="index" @click="selectOption1(item)">
                    {{ item.label }}
                  </li>
                </ul>
              </div>
              <div class="formaction">
                海洋环境噪音等级(dB//1μPa)
                <el-input v-model="NoiseLevel" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
              <div class="formaction">
                指向性指数(dB)
                <el-input v-model="DirectivityIndex" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
              <div class="formaction" v-if="showStrength">
                目标强度(dB)
                <el-input v-model="targetStrength" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
            </div>
            
            <div class="back">
              <div class="biaotou">
                <div class="biaotou-left">频率和深度</div>
              </div>
              <div class="formaction">
                频率
                <el-input v-model="Frequency" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                <div style="width: 5vw;text-align: left;color: #fff;" @click="showOptions3" @focus="onFocus"
                  @blur="onBlur" tabindex="0">
                  <div class="xialakuang">
                    <div class="selected-option">
                      {{ this.FrequencyUnit || '' }}
                    </div>
                    <img :src="require('@/assets/img/graphDown.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                      v-if="typePic4 == 0">
                    <img :src="require('@/assets/img/graphUp.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                      v-if="typePic4 == 1">
                  </div>
                </div>
                <!-- 调整下拉选项定位 -->
                <ul v-if="showOption3" class="options">
                  <li v-for="(item, index) in FrequencyUnitList" :key="index" @click="selectOption3(item)">
                    {{ item.label }}
                  </li>
                </ul>
              </div>
              <div class="formaction">
                深度
                <el-input v-model="displayValue" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                <div style="width: 5vw;text-align: left;color: #fff;" @click="showOptions4" @focus="onFocus"
                  @blur="onBlur" tabindex="0">
                  <div class="xialakuang">
                    <div class="selected-option">
                      {{ this.DepthUnit || '' }}
                    </div>
                    <img :src="require('@/assets/img/graphDown.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                      v-if="typePic5 == 0">
                    <img :src="require('@/assets/img/graphUp.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                      v-if="typePic5 == 1">
                  </div>
                </div>
                <ul v-if="showOption4" class="options">
                  <li v-for="(item, index) in DepthUnitList" :key="index" @click="selectOption4(item)">
                    {{ item.label }}
                  </li>
                </ul>
              </div>
            </div>
            <div class="back" style="margin-right: 2vw;">
              <div class="biaotou">
                <div class="biaotou-left">计算结果</div>
              </div>
              <div class="formaction" style="width: 18vw;">
                目标范围
                <el-input v-model="targetRange" autocomplete="off" @focus="onFocus" @blur="onBlur" readonly="true"
                  style="background-color: gainsboro;color: #fff;"></el-input>
                <div style="width: 5vw;text-align: left;color: #fff;" @click="showOptions5" @focus="onFocus"
                  @blur="onBlur" tabindex="0">
                  <div class="xialakuang">
                    <div class="selected-option">
                      {{ this.targetRangeUnit || '' }}
                    </div>
                    <img :src="require('@/assets/img/graphDown.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                      v-if="typePic6 == 0">
                    <img :src="require('@/assets/img/graphUp.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                      v-if="typePic6 == 1">
                  </div>
                </div>
                <ul v-if="showOption5" class="options" style="left: 12.7vw;">
                  <li v-for="(item, index) in targetRangeUnitList" :key="index" @click="selectOption5(item)">
                    {{ item.label }}
                  </li>
                </ul>
              </div>
            </div>
                  <div class="back" :style="containerStyle">
            <div class="biaotou">
              <div class="biaotou-left">声源级和信噪比</div>
            </div>
            <div class="formaction">
              声源级(dB//1μPa)
              <el-input v-model="SourceLevel" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
            </div>
            <div class="formaction">
              信噪比(dB)
              <el-input v-model="displayValue1" autocomplete="off" @focus="onFocus" @blur="onBlur" :readonly="showParams"
                :style="{ backgroundColor: showParams ? 'gainsboro' : 'transparent' }"></el-input>
            </div>
            <el-button class="button3" @click="turnMode" style="width: 20vw; margin-left: 3vw; " >{{
              this.text }}</el-button>
            <div class="biaotou" v-if="showParams">
              <div class="biaotou-left">信噪比检测参数</div>
            </div>
            <div class="formaction" v-if="showParams">
              检测概率
              <el-input v-model="Pd" autocomplete="off" @focus="onFocus" @blur="onBlur" @change="compute"></el-input>
            </div>
            <div class="formaction" v-if="showParams">
              虚警概率
              <el-input v-model="Pfa" autocomplete="off" @focus="onFocus" @blur="onBlur" @change="compute"></el-input>
            </div>
            <div class="formaction" v-if="showParams">
              脉冲数
              <el-input v-model="N" autocomplete="off" @focus="onFocus" @blur="onBlur" @change="compute"></el-input>
            </div>
            <div class="formaction" v-if="showParams">
              Swerling类型
              <div style="width: 5vw;text-align: left;color: #fff;" @click="showOptions2" @focus="onFocus"
                @blur="onBlur" tabindex="0" @change="compute">
                <div class="xialakuang">
                  <!--                  <img :src="require('@/assets/img/graphInput.png')"-->
                  <!--                    style="position: absolute;z-index: 99;width:33%;height: 80%;">-->
                  <div class="selected-option" style="margin-left: 2.8vw;">
                    {{ this.SwerlingCase || 0 }}
                  </div>
                  <img :src="require('@/assets/img/graphDown.png')"
                    style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                    v-if="typePic3 == 0">
                  <img :src="require('@/assets/img/graphUp.png')"
                    style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2vw;top: 0;"
                    v-if="typePic3 == 1">
                </div>
              </div>
              <ul v-if="showOption2" class="options">
                <li v-for="(item, index) in SwerlingCaseList" :key="index" @click="selectOption2(item)">
                  {{ item.label }}
                </li>
              </ul>
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
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Calculator',
  data() {
    return {
      calculationType: 'targetRange',
      Mode: '主动',
      NoiseLevel: 73,
      DirectivityIndex: 20,
      targetStrength: 25,
      typePic1: false,
      typePic2: false,
      typePic3: false,
      typePic4: false,
      typePic5: false,
      typePic6: false,
      Frequency: 2,
      FrequencyUnit: "kHz",
      Depth: 10000,
      DepthUnit: "m",
      text: "输入参数计算信噪比",
      showParams: false,
      SourceLevel: 220,
      SNR: 10,

      Pd: 0.81029,
      Pfa: 0.001,
      N: 1,
      SwerlingCase: 0,

      targetRangeUnit: "m",
      targetRange: 0,
      calculationTypeList: [{
        id: 1,
        value: 'targetRange',
        label: '目标探测距离'
      }],
      ModeList: [{
        id: 1,
        value: 'Active',
        label: '主动'
      },
      {
        id: 2,
        value: 'Passive',
        label: '被动'
      }],
      SwerlingCaseList: [{
        id: 1,
        value: '0',
        label: '0'
      },
      {
        id: 2,
        value: '1',
        label: '1'
      },
      {
        id: 3,
        value: '2',
        label: '2'
      },
      {
        id: 4,
        value: '3',
        label: '3'
      },
      {
        id: 5,
        value: '4',
        label: '4'
      }],
      FrequencyUnitList: [{
        id: 1,
        value: 'Hz',
        label: 'Hz'
      },
      {
        id: 2,
        value: 'kHz',
        label: 'kHz'
      },
      {
        id: 3,
        value: 'MHz',
        label: 'MHz'
      }],
      DepthUnitList: [{
        id: 1,
        value: 'm',
        label: 'm'
      },
      {
        id: 2,
        value: 'km',
        label: 'km'
      },
      {
        id: 3,
        value: 'mi',
        label: 'mi'
      },
      {
        id: 4,
        value: 'nmi',
        label: 'nmi'
      }],
      targetRangeUnitList: [{
        id: 1,
        value: 'm',
        label: 'm'
      },
      {
        id: 2,
        value: 'km',
        label: 'km'
      },
      {
        id: 3,
        value: 'mi',
        label: 'mi'
      },
      {
        id: 4,
        value: 'nmi',
        label: 'nmi'
      }],
      showOption: false,
      showOption1: false,
      showOption2: false,
      showOption3: false,
      showOption4: false,
      showOption5: false,
      showStrength: true,
      dataFinal1: {
        jsId: null,
        jsResult: {}
      },
      // pulseWidth: '1',
      // pulseWidthUnit: 'μs',
      // systemLosses: '0',
      // systemLossesUnit: 'dB',
      // noiseTemperature: '290',
      // noiseTemperatureUnit: 'K',
      // targetRadarCrossSection: '1',
      // targetRadarCrossSectionUnit: 'm²',
      // configuration: 'monostatic',
      // gain: '20',
      // gainUnit: 'dB',
      // peakTransmitPower: '1',
      // peakTransmitPowerUnit: 'kW',
      // snr: '10',
      // snrUnit: 'dB',
      // targetRange: '10.32',
      // targetRangeUnit: 'km'
    };
  },
  methods: {
    compute() {
      console.log("变化了")
      var k = null;
      if (this.SwerlingCase == 1) {
        k = 1;
      } else if (this.SwerlingCase == 2) {
        k = this.N;
      } else if (this.SwerlingCase == 3) {
        k = 2;
      } else if (this.SwerlingCase == 4) {
        k = 2 * this.N
      } else {
        k = Infinity;
      }
      var c1 = (((17.7006 * this.Pd - 18.4496) * this.Pd + 14.5339) * this.Pd - 3.525) / k;
      var c2 = (1 / k) * (Math.exp(27.31 * this.Pd - 25.14) + (this.Pd - 0.8) * (0.7 * Math.log(1e-5 / this.Pfa) + (2 * this.N - 20) / 80));
      var Cdb = null;
      if (this.Pd <= 0.872) {
        Cdb = c1;
      } else {
        Cdb = c1 + c2;
      }
      var r1 = this.shnidman_nonfluctuating();
      this.SNR = Cdb + this.pow2db(r1);
    },
    np_isscalar(element) {
      // 1. 处理 null/undefined（NumPy 会报错，这里保持一致性）
      if (element === null || element === undefined) {
        throw new TypeError("Cannot determine scalar type of null/undefined");
      }

      // 2. 获取值的内部 [[Class]]
      const type = Object.prototype.toString.call(element);

      // 3. 原生标量类型（对应 Python 的 ScalarType）
      if ([
        '[object Number]',    // 包括 new Number(5)
        '[object String]',    // 包括 new String('')
        '[object Boolean]',   // 包括 new Boolean(true)
      ].includes(type)) {
        return true;
      }

      // 4. 基本类型检测（对应 Python 的 numbers.Number）
      if (typeof element === 'number' ||
        typeof element === 'string' ||
        typeof element === 'boolean') {
        return true;
      }

      // 5. 显式排除所有对象类型（包括零维数组）
      if (type === '[object Object]' ||
        Array.isArray(element) ||
        ArrayBuffer.isView(element)) {  // 包括所有 TypedArray
        return false;
      }

      // 6. 其他情况一律视为非标量（保持与 NumPy 严格一致）
      return false;
    },
    shnidman_nonfluctuating() {
      var alpha = 0;
      if (this.N > 40) {
        alpha = 0.25;
      } else if (this.N < 0.5) {
        alpha = 0.25 - this.N / 2;
      }
      var etaPfa = Math.sqrt(-0.8 * Math.log(4 * this.Pfa * (1 - this.Pfa)))
      var etaPd = Math.sign(this.Pd - 0.5) * Math.sqrt(-0.8 * Math.log(4 * this.Pd * (1 - this.Pd)))
      var eta = null;
      if (this.np_isscalar(this.Pd) && this.np_isscalar(this.Pfa)) {
        console.log("aaa")
        eta = etaPd + etaPfa;
      } else {
        console.log("bbb")
        eta = this.outerAdd(etaPd, etaPfa);
      }
      this.SNR = (eta / this.N) * (eta + 2 * Math.sqrt(this.N / 2 + (alpha - 0.25)));
      if (Array.isArray(this.SNR)) {
        var result1 = this.SNR.map(x => Math.max(x, 0));
        this.SNR = result1;
      } else {
        this.SNR = Math.max(this.SNR, 0);
      }
      return this.SNR;
    },
    outerAdd(etaPd, etaPfa) {
      var arrA = Array.isArray(etaPd) ? etaPd : [etaPd];
      var arrB = Array.isArray(etaPfa) ? etaPfa : [etaPfa];
      var result = [];
      for (let i = 0; i < arrA.length; i++) {
        var row = [];
        for (let j = 0; j < arrB.length; j++) {
          row.push(arrA[i] + arrB[j]);
        }
        result.push(row)
      }
      return result;
    },
    pow2db(a) {
      if (a < 0) {
        this.$message.error("输入值必须为非负数");
      }
      var ydB = 10 * Math.log10(a);
      return ydB;
    },
    test() {
      this.calculationType = 'targetRange';
      this.Mode = '主动';
      this.showStrength = true;
      this.NoiseLevel = 73;
      this.DirectivityIndex = 20;
      this.targetStrength = 25;
      this.Frequency = 2;
      this.FrequencyUnit = "kHz";
      this.Depth = 10000;
      this.DepthUnit = "m";
      this.SourceLevel = 220;
      this.SNR = 10;
      this.Pd = 0.81029;
      this.Pfa = 0.001;
      this.N = 1;
      this.SwerlingCase = 0;
      this.targetRangeUnit = "m";
      this.targetRange = 0;
    },
    turnMode() {
      this.showParams = !this.showParams
    },
    clear() {
      this.calculationType = '';
      this.Mode = '';
      this.NoiseLevel = 0;
      this.DirectivityIndex = 0;
      this.targetStrength = 0;
      this.Frequency = 0;
      this.FrequencyUnit = "";
      this.Depth = 0;
      this.DepthUnit = "";
      this.SourceLevel = 0;
      this.SNR = 0;
      this.Pd = 0;
      this.Pfa = 0;
      this.N = 0;
      this.SwerlingCase = 0;
      this.targetRangeUnit = "";
      this.targetRange = 0;
      this.showParams = false;
    },
    showOptions() {
      this.showOption = !this.showOption;
      console.log(this.showOption)
      this.showOption1 = false;
      this.showOption2 = false;
      this.showOption3 = false;
      this.showOption4 = false;
      this.showOption5 = false;
      this.typePic1 = !this.typePic1;
      this.typePic2 = false;
      this.typePic3 = false;
      this.typePic4 = false;
      this.typePic5 = false;
      this.typePic6 = false;
    },
    selectOption(option) {
      this.calculationType = option.value;
      this.showOption = false;
      this.typePic1 = false;
    },
    showOptions1() {
      this.showOption1 = !this.showOption1;
      this.showOption = false;
      this.showOption2 = false;
      this.showOption3 = false;
      this.showOption4 = false;
      this.showOption5 = false;
      this.typePic2 = !this.typePic2;
      this.typePic1 = false;
      this.typePic3 = false;
      this.typePic4 = false;
      this.typePic5 = false;
      this.typePic6 = false;
    },
    selectOption1(option) {
      this.Mode = option.label;
      if (this.Mode == "主动") {
        this.showStrength = true;
      } else {
        this.showStrength = false;
      }
      this.showOption1 = false;
      this.typePic2 = false;
    },
    showOptions2() {
      this.showOption2 = !this.showOption2;
      this.showOption = false;
      this.showOption1 = false;
      this.showOption3 = false;
      this.showOption4 = false;
      this.showOption5 = false;
      this.typePic3 = !this.typePic3;
      this.typePic1 = false;
      this.typePic2 = false;
      this.typePic4 = false;
      this.typePic5 = false;
      this.typePic6 = false;
    },
    selectOption2(option) {
      this.SwerlingCase = option.value;
      this.showOption2 = false;
      this.typePic3 = false;
    },
    showOptions3() {
      this.showOption3 = !this.showOption3;
      this.showOption = false;
      this.showOption1 = false;
      this.showOption2 = false;
      this.showOption4 = false;
      this.showOption5 = false;
      this.typePic4 = !this.typePic4;
      this.typePic1 = false;
      this.typePic2 = false;
      this.typePic3 = false;
      this.typePic5 = false;
      this.typePic6 = false;
    },
    selectOption3(option) {
      this.FrequencyUnit = option.value;
      this.showOption3 = false;
      this.typePic4 = false;
    },
    showOptions4() {
      this.showOption4 = !this.showOption4;
      this.showOption = false;
      this.showOption1 = false;
      this.showOption2 = false;
      this.showOption3 = false;
      this.showOption5 = false;
      this.typePic5 = !this.typePic5;
      this.typePic1 = false;
      this.typePic2 = false;
      this.typePic3 = false;
      this.typePic4 = false;
      this.typePic6 = false;
    },
    selectOption4(option) {
      this.DepthUnit = option.value;
      this.showOption4 = false;
      this.typePic5 = false;
    },
    showOptions5() {
      this.showOption5 = !this.showOption5;
      this.showOption = false;
      this.showOption1 = false;
      this.showOption2 = false;
      this.showOption3 = false;
      this.showOption4 = false;
      this.typePic6 = !this.typePic6;
      this.typePic1 = false;
      this.typePic2 = false;
      this.typePic3 = false;
      this.typePic4 = false;
      this.typePic5 = false;
    },
    selectOption5(option) {
      this.targetRangeUnit = option.value;
      this.showOption5 = false;
      this.typePic6 = false;
    },
    onFocus(event) {
      const parentDiv = event.target.closest('.formaction');
      if (parentDiv) {
        parentDiv.classList.add('onfocus-style');
      }
    },

    onBlur(event) {
      const parentDiv = event.target.closest('.formaction');
      if (parentDiv) {
        parentDiv.classList.remove('onfocus-style');
      }
    },
    sumbitInfo() {
      if (this.SNR == undefined) {
        this.SNR = 0
      }

      // if (this.showParams) {
      //   this.SNR = this.shnidman(this.Pd, this.Pfa, this.N, this.SwerlingCase);
      // }
      var data = {
        NoiseLevel: this.NoiseLevel,
        DirectivityIndex: this.DirectivityIndex,
        Frequency: this.Frequency,
        Depth: this.Depth,
        SourceLevel: this.SourceLevel,
        SNR: this.SNR,
      }
      console.log(data)
      if (this.FrequencyUnit != "Hz") {
        if (this.FrequencyUnit == "kHz") {
          data.Frequency = this.Frequency * 1000
        }
        if (this.FrequencyUnit == "MHz") {
          data.Frequency = this.Frequency * 1000000
        }
      }
      if (this.DepthUnit != "m") {
        if (this.DepthUnit == "km") {
          data.Depth = this.Depth * 1000
        }
        if (this.DepthUnit == "mi") {
          data.Depth = this.Depth * 1609.344
        }
        if (this.DepthUnit == "nmi") {
          data.Depth = this.Depth * 1852
        }
      }
      if (this.Mode == "主动") {
        data.Mode = "Active";
        data.TargetStrength = this.targetStrength;
      } else {
        data.Mode = "Passive"
        data.TargetStrength = this.targetStrength;
      }

      console.log(data)

      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9080/snjs",//请求的后台接口
        method: "post",//get请求方式
        data: data,
        headers: {
          'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res)
        // this.targetRangeUnit = "m"
        // this.targetRange = res.data;
        if (this.targetRangeUnit == "m") {
          this.targetRange = res.data;
        }else if(this.targetRangeUnit == "km"){
          this.targetRange = res.data / 1000;
        }else if(this.targetRangeUnit == "mi"){
          this.targetRange = res.data / 1609.344;
        }else if(this.targetRangeUnit == "nmi"){
          this.targetRange = res.data / 1852;
        }
        const data1 = {
          Mode: this.Mode,
          NoiseLevel: this.NoiseLevel,
          DirectivityIndex: this.DirectivityIndex,
          TargetStrength: this.targetStrength,
          Frequency: this.Frequency,
          FrequencyUnit: "Hz",
          Depth: this.Depth,
          DepthUnit: "m",
          SourceLevel: this.SourceLevel,
          SNR: this.SNR,
          Pd: this.Pd,
          Pfa: this.Pfa,
          N: this.N,
          SwerlingCase: this.SwerlingCase,
        }
        data1.targetRange = this.targetRange;
        data1.targetRangeUnit = "m";
        this.dataFinal1.jsResult = JSON.stringify(data1);
        this.dataFinal1.jsId = this.$route.query.id;
        console.log(this.dataFinal1);
      })
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
  computed: {
    containerStyle() {
      console.log("535569")
      const div = document.getElementById("snr")
      // div.style.backgroundColor = "gainsboro";
      return {
        marginRight: '2vw',
        height: this.showParams ? '40vh' : '25vh',
        transition: 'height 0.1s ease'
      }
    },
    displayValue: {
      get(){
        if(this.Depth % 1 == 0){
          return this.Depth
        }else {
          return this.Depth.toFixed(2)
        }
      },
      set(newValue){
        console.log("111111111111")
        this.Depth = parseFloat(newValue) || 0
      }
    },
    displayValue1: {
      get(){
        if(this.SNR % 1 == 0){
          return this.SNR
        }else {
          return this.SNR.toFixed(2)
        }
      },
      set(newValue){
        this.SNR = parseFloat(newValue) || 0
      }
    }
  },
  watch: {
    SwerlingCase(newVal, oldVal) {
      if (newVal !== oldVal) {
        this.compute();
      }
    },
    FrequencyUnit(newVal, oldVal) {
      if (oldVal == "kHz" && newVal == "MHz") {
        this.Frequency = this.Frequency / 1000;
      } else if (oldVal == "kHz" && newVal == "Hz") {
        this.Frequency = this.Frequency * 1000;
      } else if (oldVal == "MHz" && newVal == "Hz") {
        this.Frequency = this.Frequency * 1e6;
      } else if (oldVal == "MHz" && newVal == "kHz") {
        this.Frequency = this.Frequency * 1000;
      } else if (oldVal == "Hz" && newVal == "MHz") {
        this.Frequency = this.Frequency / 1e6;
      } else if (oldVal == "Hz" && newVal == "kHz") {
        this.Frequency = this.Frequency / 1000;
      }
    },
    DepthUnit(newVal, oldVal) {
      if (oldVal == "m" && newVal == "km") {
        this.Depth = this.Depth / 1000;
      } else if (oldVal == "m" && newVal == "mi") {
        this.Depth = this.Depth / 1609.344;
      } else if (oldVal == "m" && newVal == "nmi") {
        this.Depth = this.Depth / 1852;
      } else if (oldVal == "km" && newVal == "m") {
        this.Depth = this.Depth * 1000;
      } else if (oldVal == "km" && newVal == "mi") {
        this.Depth = this.Depth * 1000 / 1609.344;
      } else if (oldVal == "km" && newVal == "nmi") {
        this.Depth = this.Depth * 1000 / 1852;
      } else if (oldVal == "mi" && newVal == "m") {
        this.Depth = this.Depth * 1609.344;
      } else if (oldVal == "mi" && newVal == "km") {
        this.Depth = this.Depth * 1609.344 / 1000;
      } else if (oldVal == "mi" && newVal == "nmi") {
        this.Depth = this.Depth * 1609.344 / 1852;
      } else if (oldVal == "nmi" && newVal == "m") {
        this.Depth = this.Depth * 1852;
      } else if (oldVal == "nmi" && newVal == "km") {
        this.Depth = this.Depth * 1852 / 1000;
      } else if (oldVal == "nmi" && newVal == "mi") {
        this.Depth = this.Depth * 1852 / 1609.344;
      }
    },
    targetRangeUnit(newVal, oldVal) {
      if (oldVal == "m" && newVal == "km") {
        this.targetRange = this.targetRange / 1000;
      } else if (oldVal == "m" && newVal == "mi") {
        this.targetRange = this.targetRange / 1609.344;
      } else if (oldVal == "m" && newVal == "nmi") {
        this.targetRange = this.targetRange / 1852;
      } else if (oldVal == "km" && newVal == "m") {
        this.targetRange = this.targetRange * 1000;
      } else if (oldVal == "km" && newVal == "mi") {
        this.targetRange = this.targetRange * 1000 / 1609.344;
      } else if (oldVal == "km" && newVal == "nmi") {
        this.targetRange = this.targetRange * 1000 / 1852;
      } else if (oldVal == "mi" && newVal == "m") {
        this.targetRange = this.targetRange * 1609.344;
      } else if (oldVal == "mi" && newVal == "km") {
        this.targetRange = this.targetRange * 1609.344 / 1000;
      } else if (oldVal == "mi" && newVal == "nmi") {
        this.targetRange = this.targetRange * 1609.344 / 1852;
      } else if (oldVal == "nmi" && newVal == "m") {
        this.targetRange = this.targetRange * 1852;
      } else if (oldVal == "nmi" && newVal == "km") {
        this.targetRange = this.targetRange * 1852 / 1000;
      } else if (oldVal == "nmi" && newVal == "mi") {
        this.targetRange = this.targetRange * 1852 / 1609.344;
      }
    }
  }
};
</script>

<style scoped>
.input {
  border: none;
  background-color: transparent;
  text-align: center;
  color: #fff;
  width: 8vw;
  font-size: 0.9vw;
  outline: none;
  padding: 0;
  height: 3.5vh;
}

.shuru {
  /* border: 1px solid aqua; */
  border-radius: 1vw;
  display: inline-block;
  justify-content: space-between;
  width: 8vw;
  background-image: url('@/assets/img/shurukuang.png');
  background-repeat: no-repeat;
  background-size: 98% 135%;
  background-position: 1%;
  height: 3.5vh;
}

.Info1 {
  line-height: 40px;
}

.yuan {
  width: 0.9vw;
  height: 0.9vw;
  background-color: aqua;
  border-radius: 50%;
  display: inline-block;
  justify-items: center;
}

.text {
  color: #fff;
  white-space: nowrap;
  font-size: 1vw;
  display: inline-block;
}

.select {
  background-image: url('@/assets/img/shurukuang.png');
  background-size: 100% 100%;
  background-repeat: no-repeat;
  height: 100%;
}

.comInfo {
  width: 100%;
  height: 8%;
  background-color: transparent;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/deep/ .el-select .el-input__inner {
  width: 8vw;
  text-align: center;
  background-color: transparent;
  color: #fff;
  border: none;
  font-size: 0.8vw;
}

.background-container {
  padding: 0px;
  width: 98.5%;
  height: 95%;
  background-image: none;
  background-color: #fff;
  /* 设置为视口高度 */
  background-size: cover;
  background-position: center;
  overflow: hidden;
  /* 隐藏超出背景图的内容 */
  margin-left: 1vw;
  margin-top: 2vw;
  border-radius: 30px;
}

.content-container {
  padding-left: 1vw;
  width: 100%;
  height: 100%;

  /* overflow-y: auto; */
  /* 添加垂直滚动条 */
}

.dialog-footer {
  margin-left: 65%;
  margin-bottom: 1.5%;
  display: flex;
}

.selected-option {
  text-align: center;
  font-size: 0.8vw;
  display: inline-block;
  margin-left: 0.7vw;
  width: 6vw;
  height: 100%;
  line-height: 3vh;
}

.select .el-image {
  width: 1vw;
  height: 2vh;
}

.options {
  /*border: 2px #00daff solid;*/
  width: 6.5vw;
  list-style: none;
  text-align: center;
  padding: 0;
  position: absolute;
  left: 10.7vw;
  top: 2.5vh;
  color: #fff;
  border-radius: 0.5vw;
  z-index: 99;
  font-size: 0.8vw;
  background-color: #196EC1;
  /*background-image: url('@/assets/img/optionBack.png');*/
  /*background-repeat: no-repeat;*/
  /*background-size: 100% 100%;*/
}

.options1 {
  border: 2px #00daff solid;
  width: 7.5vw;
  list-style: none;
  text-align: center;
  padding: 0;
  position: absolute;
  left: 8.3vw;
  top: 2.5vh;
  color: #fff;
  border-radius: 0.5vw;
  z-index: 99;
  font-size: 0.8vw;
}

ul :deep(li:hover) {
  background-color: #fff !important;
  color: #196EC1;
  border-radius: 0.5vw;
}

.button1 {
  border-radius: 2vw;
  line-height: 0vh;
  margin-left: 1vw;
  background-color: #196EC1;
  color: #FFFFFF;
  font-weight: bold;
}

.button2 {
  line-height: 0vh;
  margin-left: 1vw;
  background-color: #196EC1;
  color: #FFFFFF;
}

.button3 {
  line-height: 0vh;
  margin-left: 1vw;
  background-color: #f19149;
  color: #FFFFFF;
}

.waibiankuang {
  border-top: 1px solid #196EC1;
  padding-top: 2vh;
  padding-left: 1vw;
}

.formaction {
  height: 3vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 16vw;
  margin-bottom: 1vh;
  /* margin: 0 0 0.3vh; */
  padding: 0 1.2vw 0.1vh 1.5vw;
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  line-height: 3vh;
  position: relative;
  overflow: visible;
  margin-left: 1.5vw;
}


.biaotou {
  border-radius: 0.5vw;
  display: flex;
  justify-content: center;
  width: auto;
  padding: 0 0.5vw;
  margin: 0vh 0vw 0.2vh;
  margin-top: 0vh;
  margin-bottom: 1.5vh;
  background-color: #004e9c;
  height: 3vh;
  color: #fff;
}

.back {
  display: flex;
  flex-direction: column;
  height: 25vh;
  margin-bottom: 3vh;
  width: 30vw;
  border-radius: 10px;
  background-color: #006cda;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  margin-left: 2.5vw;
  margin-right: 2.5vw;
  margin-bottom: 5vh;
}

.biaotou-left {
  border-radius: 0.5vw;
  display: flex;
  justify-content: center;
  align-items: center;
  width: auto;
  padding: 0 0.5vw;
  margin: 0vh 0vw 0.2vh;
  margin-top: 0vh;
  margin-bottom: 1.5vh;
  background-color: #004e9c;
  height: 3vh;
  color: #fff;
}

.xialakuang {
  /* background-image: url('@/assets/img/xialakuang.png');
  background-size: 100% 100%; */
  /* 拉伸图像以填充整个元素 */
  /* background-repeat: no-repeat;
  background-color: transparent; */
  width: 7vw;
  height: 3vh;
  align-items: center;
  background-image: url('@/assets/img/selecter1.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  margin-left: -2vw;
}

.selected-option {
  text-align: left;
  font-size: 0.7vw;
  display: flex;
  align-items: center;
  white-space: nowrap;
  margin-left: 1vw;
  width: 3vw;
  height: 100%;
  line-height: 4vh;
}

.formaction /deep/ .el-input {
  width: 4vw;
  display: flex;
  align-items: center;
  height: 100%;
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.formaction /deep/.el-input__inner {
  text-align: center;
  padding: 0%;
  font-size: 0.9vw;
  border-radius: 0;
  width: 100%;
  height: 100%;
  color: #fff;
  border: none;
  background-color: transparent;
}
</style>
