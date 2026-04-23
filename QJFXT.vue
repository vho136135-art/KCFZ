<template>
  <div class="background-container">
    <div class="content-container">
      <div
        style="display: flex;width: 96%;margin-left: 14vw;margin-bottom: 1.5vh;margin-top: 1.5vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color: #fff; font-size: 1.6vw;font-weight: 500;">
          XXXX辅助决策
        </div>
        <el-button type="primary" class="button1" style="height: 1.5vw;margin-left: 23vw;" @click="save">保存</el-button>
      </div>
      <div style="display: flex;width: 98%;width: 96.5%;height: 87%;" class="waibiankuang">
        <div style="display: flex;flex-direction: column;width: 17vw;margin-right: 1.5vw;">
          <div style="display: flex;flex-direction: column;height: 31vh;margin-left: 0.5vw;margin-bottom: 2vh;"
            class="back">
            <div
              style="display: flex;justify-content: space-between;width: 14vw;margin-bottom: 1vh;margin-left: 1vw;margin-top: 1.5vh;"
              class="biaotou">
              <div style="vertical-align: middle;align-items: center;display: flex;">
                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                  <el-image :src="require('@/assets/img/qianbiao.png')"
                    style="display: inline-block;width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;" />
                </div>
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">环境参数设置</div>
              </div>
            </div>
            <div style="height: 80%;width: 100%;display: flex;flex-direction: column;justify-content: space-around">
              <div class="xuanzhongbeijing" tabindex="0">
                <div class="formaction">
                  <div class="text">云底高/m</div>
                  <div class="inputbg">
                    <el-input v-model="form.M" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
              </div>
              <div class="formaction">
                <div class="text">能见度/km</div>
                <div class="inputbg">
                  <el-input v-model="form.N" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div>
              <div class="formaction">
                <div class="text">真风向/°</div>
                <div class="inputbg">
                  <el-input v-model="form.B_dir" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div>
              <div class="formaction">
                <div class="text">真风速/kn</div>
                <div class="inputbg">
                  <el-input v-model="form.B_mag" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div>
              <div class="formaction">
                <div class="text">海浪波长/m</div>
                <div class="inputbg">
                  <el-input v-model="form.L" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div>
              <div class="formaction">
                <div class="text">浪向/°</div>
                <div class="inputbg">
                  <el-input v-model="form.C_dir_0" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div>
            </div>
          </div>
          <div class="back1" style="height: 34.2vh;margin-left: 0.5vw;display: flex;flex-direction: column;">
            <div
              style="display: flex;justify-content: space-between;width: 14vw;margin-bottom: 2vh;margin-left: 1vw;margin-top: 1.5vh;"
              class="biaotou">
              <div style="vertical-align: middle;align-items: center;display: flex;">
                <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                  <el-image :src="require('@/assets/img/qianbiao.png')"
                    style="display: inline-block;width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;" />
                </div>
                <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">仿真控制</div>
              </div>
            </div>
            <div style="display: flex;flex-direction: column;justify-content:space-between;">
              <div class="buttonLeft" style="display: inline-block;margin-left:1vw;width: 11vw;">
                <el-button style="font-size: 0.8vw;" @click="test">载入测试值</el-button>
              </div>
              <div class="buttonRight" style="margin-left:4vw;width: 11vw;display: inline-block;">
                <el-button style="font-size: 0.8vw;margin-left: -1vw;" @click="dataInitialize">数据初始化</el-button>
              </div>
              <div class="buttonLeft" style="display: inline-block;margin-left:1vw;width: 11vw;">
                <el-button style="font-size: 0.8vw;" @click="submitForm">计算</el-button>
              </div>
              <div class="buttonRight" style="margin-left:4vw;width: 11vw;display: inline-block;">
                <el-button style="font-size: 0.8vw;margin-left: -1vw;" @click="clearImage">清除数据</el-button>
              </div>
            </div>
          </div>
        </div>
        <div style="display: flex;flex-direction: column;width: 57vw;">
          <div style="display: flex;margin-bottom: 2vh;">
            <div style="display: flex;flex-direction: column;width: 25vw;height: 37vh;margin-right: 1.5vw;"
              class="back2">
              <div
                style="display: flex;justify-content: space-between;width: 23vw;margin-bottom: 1vh;margin-left: 1vw;margin-top: 1.5vh;"
                class="biaotou">
                <div style="vertical-align: middle;align-items: center;display: flex;">
                  <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                    <el-image :src="require('@/assets/img/qianbiao.png')"
                      style="display: inline-block;width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;" />
                  </div>
                  <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">舰艇选择与参数设置</div>
                </div>
              </div>
              <div style="height: 85%;width: 100%;display: flex;flex-direction: column;justify-content: space-around">
                <div class="formaction1">
                  <div class="text">舰艇</div>
                  <div style="width: 5vw;text-align: left;color: #fff;" @click="showOptions" @focus="onFocus1"
                    @blur="onBlur1" tabindex="0">
                    <div class="xialakuang">
                      <img :src="require('@/assets/img/graphInput.png')"
                        style="position: absolute;z-index: 99;width:20%;height: 80%;">
                      <div class="selected-option">
                        {{ this.form.ship_type || '' }}
                      </div>
                      <img :src="require('@/assets/img/graphDown.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 0.6vw;top: 0;"
                        v-if="typePic1 == 0">
                      <img :src="require('@/assets/img/graphUp.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 0.6vw;top: 0;"
                        v-if="typePic1 == 1">
                      <!-- <el-image :src="require('@/assets/img/xiala.png')"></el-image> -->
                    </div>
                  </div>
                  <ul v-if="showOptions2" class="options">
                    <li v-for="(option, index) in shipList" :key="index" @click="selectOption2(option)">
                      {{ option.label }}
                    </li>
                  </ul>
                </div>
                <div class="formaction1">
                  <div class="text">舰载直升机</div>
                  <div style="width: 5vw;text-align: left;color: #fff;" @click="showOptions1" @focus="onFocus1"
                    @blur="onBlur1" tabindex="0">
                    <div class="xialakuang">
                      <img :src="require('@/assets/img/graphInput.png')"
                        style="position: absolute;z-index: 99;width:20%;height: 80%;">
                      <div class="selected-option">
                        {{ this.form.heli_type || '' }}
                      </div>
                      <img :src="require('@/assets/img/graphDown.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 0.6vw;top: 0;"
                        v-if="typePic2 == 0">
                      <img :src="require('@/assets/img/graphUp.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 0.6vw;top: 0;"
                        v-if="typePic2 == 1">
                      <!-- <el-image :src="require('@/assets/img/xiala.png')"></el-image> -->
                    </div>
                  </div>
                  <ul v-if="showOptions3" class="options">
                    <li v-for="(option, index) in heliList" :key="index" @click="selectOption3(option)">
                      {{ option.label }}
                    </li>
                  </ul>
                </div>
                <div class="formaction1">
                  <div class="text">是否使用助降设备</div>
                  <div style="width: 5vw;text-align: left;color: #fff;display: flex;align-items: center;"
                    @focus="onFocus1" @blur="onBlur1" tabindex="0" @click="showOptions5">
                    <div class="xialakuang">
                      <img :src="require('@/assets/img/graphInput.png')"
                        style="position: absolute;z-index: 99;width:20%;height: 80%;">
                      <div class="selected-option">
                        {{ this.form.zjsb || '' }}
                      </div>
                      <img :src="require('@/assets/img/graphDown.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 0.6vw;top: 0;"
                        v-if="typePic3 == 0">
                      <img :src="require('@/assets/img/graphUp.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 0.6vw;top: 0;"
                        v-if="typePic3 == 1">
                      <!-- <el-image :src="require('@/assets/img/xiala.png')"></el-image> -->
                    </div>
                    <el-checkbox v-model="form.useZjsb" style="margin-left: 1.5vw;"></el-checkbox>
                  </div>
                  <ul v-if="showOptions4" class="options">
                    <li v-for="(option, index) in zjsbList" :key="index" @click="selectOption4(option)">
                      {{ option.label }}
                    </li>
                  </ul>
                </div>
                <div class="formaction1" style="width: 22vw;">
                  <div class="text">当前横摇/°</div>
                  <div class="inputbg">
                    <el-input v-model="form.Y" autocomplete="off" @focus="onFocus1" @blur="onBlur1"></el-input>
                  </div>
                </div>
                <div class="formaction1" style="width: 22vw;">
                  <div class="text">当前纵摇/°</div>
                  <div class="inputbg">
                    <el-input v-model="form.Z" autocomplete="off" @focus="onFocus1" @blur="onBlur1"></el-input>
                  </div>
                </div>
                <div class="formaction1" style="width: 22vw;">
                  <div class="text">当前航向/°</div>
                  <div class="inputbg">
                    <el-input v-model="form.A_dir" autocomplete="off" @focus="onFocus1" @blur="onBlur1"></el-input>
                  </div>
                </div>
                <div class="formaction1" style="width: 22vw;">
                  <div class="text">当前航速/kn</div>
                  <div class="inputbg">
                    <el-input v-model="form.A_mag" autocomplete="off" @focus="onFocus1" @blur="onBlur1"></el-input>
                  </div>
                </div>
                <div class="formaction1" style="width: 22vw;">
                  <div class="text">纵摇周期/s</div>
                  <div class="inputbg">
                    <el-input v-model="form.T" autocomplete="off" @focus="onFocus1" @blur="onBlur1"></el-input>
                  </div>
                </div>
              </div>

            </div>
            <div class="back4">
              <div
                style="height: 99%;width: 98%;border-radius: 0.5vw;margin-left: 1%;margin-top: 0.5%;display: flex;justify-content: center;">
                <!-- <div id="chart-container" style="width: 100%;background-color: transparent !important;"></div> -->
                <img :src="src" style="width: 100%;justify-items: center;justify-content: center"
                  @click="showBigInfo" />
                <!--                <img src="../../assets/plot2.png" />-->
              </div>

            </div>
          </div>
          <div style="display: flex;">
            <div
              style="width: 26vw;margin-right: 1.5vw;border-radius: 1vw;display: flex;height: 28.4vh;flex-direction: column;"
              class="back3">
              <div
                style="display: flex;justify-content: space-between;width: 24vw;margin-bottom: 2vh;margin-left: 1vw;margin-top: 1.5vh;"
                class="biaotou">
                <div style="vertical-align: middle;align-items: center;display: flex;">
                  <div style="display: flex;align-items: baseline;height: 100%;" class="biaotouqian">
                    <el-image :src="require('@/assets/img/qianbiao.png')"
                      style="display: inline-block;width: 0.6vw;margin-left: 1vw;margin-right: 0.4vw;height: 100%;" />
                  </div>
                  <div style="color: #fff; text-align: left;white-space: nowrap;font-size: 0.9vw;">计算结果输出</div>
                </div>
              </div>
              <div style="display: flex;flex-wrap: wrap; gap: 0.8vw 2vw;">
                <div
                  style="height: 7.5vh; width: 10vw;margin-left: 1vw; margin-right: 2vw;display: flex; flex-direction: column;"
                  class="biankuang">
                  <div style="display: block; text-align: left; margin-left: 1vw;height: 4vh;">
                    <div
                      style="color: #fff; font-size: 0.8vw;height: 2vh; margin-top: 1.3vh; display: inline-block; white-space: nowrap;">
                      合成风向/°
                    </div>
                  </div>
                  <div style="display: flex;height: 3.5vh; justify-content: flex-end;width: 9.5vw;">
                    <el-input v-model="formTiao.R_1" autocomplete="off" readonly></el-input>
                    <div style="color: aqua; font-size: 1.2vw;">
                      °
                    </div>
                  </div>
                </div>
                <div style="height: 7.5vh; width: 10vw; display: inline-block;display: flex; flex-direction: column; "
                  class="biankuang">
                  <div style="display: block; text-align: left; margin-left: 1vw;height: 4vh;">
                    <div
                      style="color: #fff; font-size: 0.8vw;height: 2vh; margin-top: 1.3vh; display: inline-block; white-space: nowrap;">
                      合成风速/kn
                    </div>
                  </div>
                  <div style="display: flex;height: 3.5vh; justify-content: flex-end;width: 9.5vw;">


                    <el-input v-model="formTiao.R_mag" autocomplete="off" readonly></el-input>
                    <div style="color: aqua; font-size: 0.8vw;">
                      kn
                    </div>
                  </div>
                </div>
                <div
                  style="height: 7.5vh; width: 10vw; display: inline-block;margin-left: 1vw; margin-right: 2vw; display: flex; flex-direction: column;"
                  class="biankuang">
                  <div style="display: block; text-align: left; margin-left: 1vw;height: 4vh;">
                    <div
                      style="color: #fff; font-size: 0.8vw;height: 2vh; margin-top: 1.3vh; display: inline-block; white-space: nowrap;">
                      能否起降
                    </div>
                  </div>
                  <div style="display: flex;height: 3.5vh; width: 10vw;" class="info1111"
                    v-if="formTiao.qj == '不能起降，需要调整'">
                    <div style="display: flex; align-items: center;height: 2vh;font-size: 0.8vw;">
                      <el-input v-model="formTiao.qj" autocomplete="off" style="width: 100%;" readonly></el-input>
                    </div>
                  </div>
                  <div style="display: flex;height: 3.5vh; width: 10vw;" class="info1111" v-if="formTiao.qj == '不能起降'">
                    <div style="display: flex; align-items: center;height: 2vh;font-size: 0.8vw;">
                      <el-input v-model="formTiao.qj" autocomplete="off" style="width: 100%;" readonly></el-input>
                    </div>
                  </div>
                  <div style="display: flex;height: 3.5vh; width: 10vw;" class="info1111K" v-if="formTiao.qj == '能'">
                    <div style="display: flex; align-items: center;height: 2vh;font-size: 0.8vw;">
                      <el-input v-model="formTiao.qj" autocomplete="off" style="width: 100%;" readonly></el-input>
                    </div>
                  </div>
                </div>
                <div style="height: 7.5vh; width: 10vw; display: inline-block;display: flex; flex-direction: column;"
                  class="biankuang">
                  <div style="display: block; text-align: left; margin-left: 1vw;height: 3vh;">
                    <div
                      style="color: #fff; font-size: 0.8vw; height: 2vh; margin-top: 1.3vh; display: inline-block; white-space: nowrap;">
                      原因
                    </div>
                  </div>
                  <div style="display: flex; height: 3.5vh; justify-content: flex-end;width: 8.5vw;">
                    <div style="display: flex; align-items: center;height: 3.5vh;">
                      <el-input style="width: 8.5vw;margin-left: 0.5vw" v-model="formTiao.yy" autocomplete="off"
                        class="yyinput" readonly></el-input>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div style="height: 28.4vh;width: 29vw;border-radius: 1vw;display: flex;flex-wrap: wrap;" class="back5">
              <div
                style="height: 7.5vh; width: 8vw;display: flex; flex-direction: column;margin-top: 5vh;margin-left: 2vw;margin-bottom: 0; "
                class="biankuang">
                <div style="display: block; text-align: left; margin-left: 1vw;height: 4vh;">
                  <div
                    style="color: #fff; font-size: 0.8vw;height: 2vh; margin-top: 1.3vh; display: inline-block; white-space: nowrap;">
                    期望风速/kn
                  </div>
                </div>
                <div style="display: flex;height: 3.5vh; justify-content: flex-end;width: 7.8vw;">
                  <el-input v-model="form.target_R_mag" autocomplete="off"></el-input>
                  <div style="color: aqua; font-size: 0.8vw;">
                    kn
                  </div>
                </div>
              </div>
              <!-- <div class="buju">
                <div class="yibiaopan">
                  <el-image :src="require('@/assets/img/yipan.png')" class="yibiaopantupian" />
                  <div style="display: flex;align-items: center;height: 2vw;" class="yibiaowenzi">
                    <input v-model="form.target_R_mag"
                      style="width: 1.5vw;background: transparent;border: none;font-size: 1.25vw;color: aqua;text-align: center;outline: none;" />
                    <span
                      style="color: aqua;font-size: 1.25vw;white-space: nowrap;position: relative; top: -0.1vw;">/kn</span>
                  </div>
                </div>
                <div class="yuanju">期望风速/kn</div>
              </div> -->
              <div class="buju" style="margin-left: 1.9vw;">
                <div class="yibiaopan">
                  <el-image :src="require('@/assets/img/yipan.png')" class="yibiaopantupian" />
                  <div style="display: flex;align-items: center;height: 2vw;left: 27%;" class="yibiaowenzi">

                    <input v-model="formTiao.tz" v-if="formTiao.tz == '能'"
                      style="width: 2.5vw;background: transparent;border: none;font-size: 1.25vw;color: #91ff67;text-align: center;outline: none;" />
                    <input v-model="formTiao.tz" v-if="formTiao.tz == '不能'"
                      style="width: 2.5vw;background: transparent;border: none;font-size: 1.25vw;color: #ff5a3c;text-align: center;outline: none;" />
                  </div>
                </div>
                <div class="yuanju">能否调整</div>
              </div>
              <div class="buju">
                <div class="yibiaopan">
                  <el-image :src="require('@/assets/img/yipan.png')" class="yibiaopantupian" />
                  <div style="display: flex;align-items: center;height: 2vw;left: 35%;" class="yibiaowenzi">
                    <input v-model="formTiao.A3" readonly
                      style="width: 1.5vw;background: transparent;border: none;font-size: 1.25vw;color: #fff053;text-align: center;outline: none;" />
                    <span
                      style="color: #fff053;font-size: 1.25vw;white-space: nowrap;position: relative; top: -0.1vw;">°</span>
                  </div>
                </div>
                <div class="yuanju">航向/°</div>
              </div>
              <div class="buju">
                <div class="yibiaopan">
                  <el-image :src="require('@/assets/img/yipan.png')" class="yibiaopantupian" />
                  <div style="display: flex;align-items: center;height: 2vw;    margin-top: 10%;" class="yibiaowenzi">
                    <div
                      style="width: 100%;background: transparent;border: none;font-size: 1.25vw;color: #ff7349;text-align: center;outline: none;">
                      {{ formTiao.V1 }}</div>
                  </div>
                </div>
                <div class="yuanju">谐振航速/kn</div>
              </div>
              <div
                style="color: #fff;display: flex;justify-content: center;align-items: center;margin-left: 1vw;font-size: 2vw;height: 5.8vw;margin-top: 1.4vh;">
                ~</div>
              <div class="buju" style="margin-left: 1vw;">
                <div class="yibiaopan">
                  <el-image :src="require('@/assets/img/yipan.png')" class="yibiaopantupian" />
                  <div style="display: flex;align-items: center;height: 2vw;    margin-top: 10%;" class="yibiaowenzi">
                    <div
                      style="width: 100%;background: transparent;border: none;font-size: 1.25vw;color: #ff7349;text-align: center;outline: none;">
                      {{ formTiao.V2 }}</div>

                  </div>
                </div>
                <div class="yuanju">谐振航速/kn</div>
              </div>
              <div class="buju">
                <div class="yibiaopan">
                  <el-image :src="require('@/assets/img/yipan.png')" class="yibiaopantupian" />
                  <div style="display: flex;align-items: center;height: 2vw;    margin-top: 10%;" class="yibiaowenzi">
                    <input v-model="formTiao.A_adj_mag" readonly
                      style="width: 1.5vw;background: transparent;border: none;font-size: 1.25vw;color: #ff4949;text-align: center;outline: none;" />
                    <!--                    <span-->
                    <!--                      style="color: #ff4949;font-size: 1.25vw;white-space: nowrap;position: relative; top: -0.1vw;">/kn</span>-->
                  </div>
                </div>
                <div class="yuanju">航速/kn</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <el-dialog title="预览" :visible.sync="showBig">
        <div style="height: 20vw;width: 100%;margin: 0 auto;display: flex;justify-content: center;" class="imgContainer"
          @wheel.prevent="handleWheel" @mousedown="startDrag" @mousemove="handleDrag" @mouseup="endDrag">
          <img :src="src" style="height: 100%;object-fit: contain;" :style="{
            transform: `scale(${scale}) translate(${dragOffset.x}px, ${dragOffset.y}px)`,
            cursor: isDragging ? 'grabbing' : 'grab'
          }" class="showBig">
        </div>

      </el-dialog>



      <div class="loader" v-if="showJZ"></div>
    </div>
  </div>
</template>

<script>



export default {
  data() {
    return {
      showBig: false,
      urls: [],
      showJZ: false,
      isVisible: true,
      isVisible1: false,
      isVisibleTiao: false,
      answerType: 0,
      scale: 1,
      isDragging: false,
      dragStart: { x: 0, y: 0 },
      dragOffset: { x: 0, y: 0 },
      lastOffset: { x: 0, y: 0 },
      typePic1: 0,
      typePic2: 0,
      typePic3: 0,
      showOptions2: false,
      showOptions3: false,
      showOptions4: false,
      dataFinal1: {
        jsId: null,
        jsResult: {}
      },
      shipList: [{
        id: 1,
        value: '054A护卫舰',
        label: 'A'
      },
      {
        id: 2,
        value: '052D驱逐舰',
        label: 'B'
      },
      {
        id: 3,
        value: '055驱逐舰',
        label: 'C'
      }],
      heliList: [{
        id: 1,
        value: 'D',
        label: 'A1'
      },
      {
        id: 2,
        value: 'E',
        label: 'B1'
      },
      {
        id: 3,
        value: 'G',
        label: 'C1'
      },
      {
        id: 4,
        value: 'F',
        label: 'D1'
      }],
      zjsbList: [{
        id: 1,
        value: '鱼叉',
        label: '鱼叉'
      },
      {
        id: 2,
        value: '助降网',
        label: '助降网'
      },
      {
        id: 3,
        value: '拉降系统',
        label: '拉降系统'
      }],
      src: '',
      form: {
        A_mag: 0,
        A_dir: 0,
        B_mag: 0,
        B_dir: 0,
        C_dir_0: 0,
        T: 0,
        L: 0,
        ship_type: "",
        heli_type: "",
        target_R_mag: 0,
        zjsb: "",
        useZjsb: false,
        M: 0,
        N: 0,
        Y: 0,
        Z: 0,
        yy: "",
      },
      formTiao: {
        A_adj_mag: 0,
        A2: 0,
        A3: 0,
        V1: 0,
        V2: 0,
        R_1: 0,
        R_mag: 0,
        qj: "",
        tz: "",
        yy: "",
      },
      data: {

      },
    };
  },
  methods: {
    showBigInfo() {
      this.showBig = true;

    },
    clearImage() {
      this.src = "";
      this.form.M = 0;
      this.form.N = 0;
      this.form.B_dir = 0;
      this.form.B_mag = 0;
      this.form.L = 0;
      this.form.C_dir_0 = 0;
      this.form.ship_type = '';
      this.form.heli_type = '';
      this.form.useZjsb = false;
      this.form.zjsb = ""
      this.form.Y = 0;
      this.form.Z = 0;
      this.form.A_dir = 0;
      this.form.A_mag = 0;
      this.form.T = 0;

      this.form.target_R_mag = 0
      this.formTiao = {
        A_adj_mag: 0,
        A2: 0,
        A3: 0,
        V1: 0,
        V2: 0,
        R_1: 0,
        R_mag: 0,
        qj: "",
        tz: "",
        yy: "",
      }
    },
    handleWheel(e) {
      // 计算缩放比例
      const delta = e.deltaY > 0 ? -0.1 : 0.1;
      this.scale += delta;

      // 限制缩放范围
      this.scale = Math.min(Math.max(0.5, this.scale), 3);
    },
    startDrag(e) {
      this.isDragging = true;
      this.dragStart = { x: e.clientX, y: e.clientY };
    },
    handleDrag(e) {
      if (this.isDragging) {
        console.log(this.isDragging)
        console.log("222222222")
        // 计算当前鼠标位置与起始位置的差值
        const offsetX = e.clientX - this.dragStart.x;
        const offsetY = e.clientY - this.dragStart.y;

        // 更新拖拽偏移量
        this.dragOffset = {
          x: this.lastOffset.x + offsetX,
          y: this.lastOffset.y + offsetY
        };
      }
    },
    endDrag() {
      if (this.isDragging) {
        this.isDragging = false; // 停止拖拽
        console.log(this.isDragging)
        this.lastOffset = { ...this.dragOffset }; // 保存当前偏移量
      }
    },
    dataInitialize() {
      this.src = "";
      if (this.data.zjsb != "") {
        this.data.useZjsb = true;
      }
      // this.form = {
      //   A_mag: 0,
      //   A_dir: 0,
      //   B_mag: 0,
      //   B_dir: 0,
      //   C_dir_0: 0,
      //   T: 0,
      //   L: 0,
      //   Y: 0,
      //   Z: 0,
      //   M: 0,
      //   N: 0,
      //   ship_type: "",
      //   heli_type: "",
      //   zjsb: "",
      //   useZjsb: false,
      //   target_R_mag: 0,
      // },
      this.form.M = this.data.M;
      this.form.N = this.data.N;
      this.form.B_dir = this.data.B_dir;
      this.form.B_mag = this.data.B_mag;
      this.form.L = this.data.L;
      this.form.C_dir_0 = this.data.C_dir_0;
      this.form.ship_type = this.data.ship_type;
      this.form.heli_type = this.data.heli_type;
      this.form.useZjsb = this.data.useZjsb;
      this.form.zjsb = this.data.zjsb;
      this.form.Y = this.data.Y;
      this.form.Z = this.data.Z;
      this.form.A_dir = this.data.A_dir;
      this.form.A_mag = this.data.A_mag;
      this.form.T = this.data.T;

      this.form.target_R_mag = 0;
      this.formTiao = {
        A_adj_mag: 0,
        A2: 0,
        A3: 0,
        V1: 0,
        V2: 0,
        R_1: 0,
        R_mag: 0,
        qj: "",
        tz: "",
        yy: "",
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
      this.typePic1 = !this.typePic1;
      this.typePic2 = false;
      this.typePic3 = false;
    },
    showOptions1() {
      this.showOptions3 = !this.showOptions3;
      this.showOptions2 = false;
      this.showOptions4 = false;
      this.typePic2 = !this.typePic2;
      this.typePic1 = false;
      this.typePic3 = false;
    },
    showOptions5() {
      this.showOptions4 = !this.showOptions4;
      this.showOptions2 = false;
      this.showOptions3 = false;
      this.typePic3 = !this.typePic3;
      this.typePic1 = false;
      this.typePic2 = false;
    },
    selectOption2(option) {
      this.form.ship_type = option.value;
      console.log(this.form.ship_type)
      this.showOptions2 = false;
      this.typePic1 = false;
    },
    selectOption3(option) {
      this.form.heli_type = option.value;
      this.showOptions3 = false;
      this.typePic2 = false;
    },
    selectOption4(option) {
      this.form.zjsb = option.value;
      this.showOptions4 = false;
      this.typePic3 = false;
    },
    submitForm() {
      this.showJZ = true;
      var dataFinal = {
        "ship_type": this.form.ship_type,
        "A_mag": this.form.A_mag,
        "A_dir": this.form.A_dir,
        "heli_type": this.form.heli_type,
        "B_mag": this.form.B_mag,
        "B_dir": this.form.B_dir,
        "T": this.form.T,
        "L": this.form.L,
        "Y": this.form.Y,
        "Z": this.form.Z,
        "M": this.form.M,
        "N": this.form.N,
        "zjsb": "无",
        "C_dir_0": this.form.C_dir_0,
        "target_R_mag": this.form.target_R_mag,
      }
      if (this.form.useZjsb) {
        dataFinal.zjsb = this.form.zjsb;
      }
      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9080/qjfxtJk",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {

          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res)
        if (res.data.qj == "不能起降，需要调整") {
          if (res.data.yy != "位于谐振航速区间") {
            this.formTiao.yy = res.data.yy
            this.formTiao.qj = "不能起降，需要调整"
            this.formTiao.R_1 = res.data.R_1
            this.formTiao.R_mag = res.data.R_mag
            this.formTiao.V1 = res.data.V1
            this.formTiao.V2 = res.data.V2
            if(res.data.tz == "可以调整"){
              this.formTiao.tz = "能"
            }
            this.urls.push(res.data.png1)
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
              console.log(this.src)
              this.showJZ = false
              this.urls = []
            })
          }else {
            this.formTiao.yy = res.data.yy
            this.formTiao.qj = "不能起降，需要调整"
            this.formTiao.R_1 = res.data.R_1
            this.formTiao.R_mag = res.data.R_mag
            this.formTiao.V1 = res.data.V1
            if(res.data.tz == "可以调整"){
              this.formTiao.tz = "能"
            }
            this.formTiao.A_adj_mag = res.data.A_adj_mag
            this.formTiao.V2 = res.data.V2
            this.formTiao.A3 = res.data.A3
            console.log(res.data.png2)
            this.urls.push(res.data.png2)
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
              console.log(res)
              this.src = res.data.results[0].url;
              console.log(this.src)
              this.showJZ = false
              this.urls = []
            })
          }
        }
        else if (res.data.qj == "已经调整" && res.data.tz != "无法调整") {
          this.formTiao.qj = "可以起降"
          this.answerType = 0;
          this.formTiao.A_adj_mag = res.data.A_adj_mag
          this.formTiao.R_1 = res.data.R_1
          this.formTiao.R_mag = res.data.R_mag
          this.formTiao.V1 = res.data.V1
          this.formTiao.yy = ""
          this.formTiao.V2 = res.data.V2
          this.formTiao.qj = "能"
          this.formTiao.tz = res.data.tz
          this.answerType = 1;
          this.urls.push(res.data.png1);
          if (res.data.tz == "可以调整") {
            this.formTiao.tz = "能";
            this.formTiao.A_adj_mag = res.data.A_adj_mag;
            this.formTiao.A3 = res.data.A3;
            this.urls.push(res.data.png2);
          }
          // this.urls.push(res.data.png3);
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
            this.src = res.data.results[1].url;
            const combinedData = {
              ...this.form,
              ...this.formTiao,
            };
            this.dataFinal1.jsResult = JSON.stringify(combinedData),
              this.dataFinal1.jsId = this.$route.query.id;
            this.dataFinal1.allImg = this.src + "," + this.src1;
            console.log(this.dataFinal1);
          }).finally(() => {
            this.showJZ = false;
            this.urls = [];
          })
        }
        else if (res.data.qj == "不能起降") {
          this.formTiao.qj = res.data.qj
          this.formTiao.yy = res.data.yy
          this.showJZ = false
        }
        else {
          this.answerType = 0;
          // this.formTiao.A_adj_mag = res.data.A_adj_mag
          this.formTiao.R_1 = res.data.R_1
          this.formTiao.R_mag = res.data.R_mag
          this.formTiao.V1 = res.data.V1
          this.formTiao.V2 = res.data.V2
          this.formTiao.qj = "能"
          this.formTiao.tz = res.data.tz
          this.answerType = 1;
          this.urls.push(res.data.png1);
          if (res.data.tz == "调整后") {
            this.formTiao.tz = "能";
            this.formTiao.A_adj_mag = res.data.A_adj_mag;
            this.formTiao.A3 = res.data.A3;
            this.urls.push(res.data.png2);
          }
          this.urls.push(res.data.png3);
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
            console.log(this.src)
            this.src1 = res.data.results[1].url;
            const combinedData = {
              ...this.form,
              ...this.formTiao,
            };
            this.dataFinal1.jsResult = JSON.stringify(combinedData),
              this.dataFinal1.allImg = this.src + "," + this.src1;
            this.dataFinal1.jsId = this.$route.query.id;
            console.log(this.dataFinal1);
          }).finally(() => {
            this.showJZ = false
          })
        }
      })
    },
    test() {
      this.form.M = 500;
      this.form.N = 6;
      this.form.B_dir = 60;
      this.form.B_mag = 12;
      this.form.L = 100;
      this.form.C_dir_0 = 10;
      this.form.ship_type = '052D驱逐舰';
      this.form.heli_type = 'E';
      this.form.useZjsb = true;
      this.form.zjsb = "鱼叉"
      this.form.Y = 2;
      this.form.Z = 2;
      this.form.A_dir = 0;
      this.form.A_mag = 18;
      this.form.T = 5;
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
      if (newVal == '055驱逐舰') {
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
      } else if (newVal == 'F') {
        this.form.zjsb = '拉降系统';
      }
    }
  },
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
  width: 4.5vw;
  list-style: none;
  text-align: center;
  padding: 0;
  position: absolute;
  left: 18.4vw;
  top: 2vh;
  color: #fff;
  border-radius: 0.5vw;
  z-index: 100;
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
  color: #fff;
  border: none;
  background-color: transparent;
}

/deep/.el-input {
  width: 6vw;
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
  background-color: transparent;
  border: none;
  width: 100%;
  color: #fb2f0d;
}

.info1111K /deep/ .el-input__inner {
  font-size: 0.8vw;
  height: 100%;
  background-color: transparent;
  border: none;
  width: 100%;
  color: #19ff00;
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
  font-size: 0.8vw;
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
  width: 100%;
  /* height: 100%; */
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

.formaction {
  height: 3vh;
  display: flex;
  justify-content: space-between;
  width: 13.5vw;
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
  background-image: url('@/assets/img/wbk.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  padding-top: 2vh;
  padding-left: 1vw;
}

.inputbg .el-input {
  width: 4vw;
  margin-right: 1vw;
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.yibiaowenzi {
  text-align: center;
  width: 100%;
  justify-content: center;
}

.showBig {
  max-width: 100%;
  max-height: 100%;
  transition: transform 0.1s ease;
}

.imgContainer {
  overflow: hidden;
}
</style>
