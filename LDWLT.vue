<template>
  <div class="background-container">
    <div class="content-container">
      <!--顶部横条-->
      <div
          style="display: flex;width: 96%;margin-bottom: 1.5vh;margin-top: 1.5vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color:#196EC1; font-size: 1.6vw;font-weight: 500;">
          大气波导对电磁场传播的影响分析软件
        </div>
        <!--        <el-button class="button1" style="height: 1.5vw;margin-left: 33vw;" @click="save">保存</el-button>-->
      </div>
      <div style="display: flex;width: 96.5%;height: 90%;" class="waibiankuang">
        <!--下方整体-->
        <div class="allInf01" style="display: flex;">

          <!--左侧三个-->
          <div style="display: flex;flex-direction: column;width: 19vw;margin-right: 0.7vw;margin-left: 1vw;">
            <div class="back">
              <div class="biaotou">
                <div class="biaotou-left">范围参数</div>
              </div>
              <div>
                <div class="formaction">
                  最大距离 (km)
                  <el-input style="margin-right: 1vw;" v-model="maxRange" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
                <div class="formaction">
                  最大高度 (m)
                  <el-input style="margin-right: 1vw;" v-model="maxAltitude" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div>
            </div>
            <div class="back">
              <div class="biaotou">
                <div class="biaotou-left">TX天线参数</div>
              </div>
              <div class="formaction">
                极化
                <div class="selectInfo1" style="width: 6vw;" @click="showOptions" @focus="onFocus"
                  @blur="onBlur" tabindex="0">
                  <div class="xialakuang">
                    <img :src="require('@/assets/img/graphInput.png')"
                      style="position: absolute;z-index: 99;width:20%;height: 80%;">
                    <div class="selected-option">
                      {{ getLabel(polarization, polarizationList) || '' }}
                    </div>
                    <img :src="require('@/assets/img/graphDown.png')"
                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 1.8vw;top: 0;"
                      v-if="typePic1 == 0">
                    <img :src="require('@/assets/img/graphUp.png')"

                      style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 1.8vw;top: 0;"
                      v-if="typePic1 == 1">
                  </div>
                </div>
                <!-- 调整下拉选项定位 -->
                <ul v-if="showOption" class="options">
                  <li v-for="(item, index) in polarizationList" :key="index" @click="selectOption(item)">
                    {{ item.label }}
                  </li>
                </ul>
              </div>
              <div class="formaction">
                3dB波束宽度 (deg)
                <el-input  style="margin-right: 1vw;" v-model="beamwidth" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
              <div class="formaction">
                仰角 (deg)
                <el-input  style="margin-right: 1vw;" v-model="elevation_angle" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
              <div class="formaction">
                天线高度 (m)
                <el-input  style="margin-right: 1vw;" v-model="antenna_height" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
              <div class="formaction">
                频率 (MHz)
                <el-input  style="margin-right: 1vw;" v-model="frequency" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>

            </div>
            <div class="back">
              <div class="biaotou">
                <div class="biaotou-left">大气参数</div>
              </div>
              <div>
                <div class="formaction">
                  <el-radio v-model="refractivity_type" label="Range-indep. refractivity" @input="onFocus"
                    @blur="onBlur">范围索引折射率
                  </el-radio>
                </div>
                <div class="formaction" style="padding-right: 3vw;width:13vw">
                  类型
                  <div class="selectInfo1" @click="showAtmosphereOption" @focus="onFocus"
                    @blur="onBlur" tabindex="0">
                    <div class="xialakuang" style="width: 5vw;margin-left: 3vw;">
                      <img :src="require('@/assets/img/graphInput.png')"
                        style="position: absolute;z-index: 99;width:28%;height: 80%;">
                      <div class="selected-option" style="margin-left: 0.5vw">
                        {{ getLabel(refractivity_type_combobox, atmosphereTypeList) || '' }}
                      </div>
                      <img :src="require('@/assets/img/graphDown.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 1.5vw;top: 0;"
                        v-if="typePic2 == 0">
                      <img :src="require('@/assets/img/graphUp.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 1.5vw;top: 0;"
                        v-if="typePic2 == 1">
                    </div>
                  </div>
                  <ul v-if="atmosphereOption" class="options" style="width: 4.2vw;right: 1.3vw">
                    <li v-for="(item, index) in atmosphereTypeList" :key="index" @click="selectAtmosphereOption(item)">
                      {{ item.label }}
                    </li>
                  </ul>
                </div>
                <div class="formaction">
                  <el-radio v-model="refractivity_type" label="Range-dep.refractivity">远距折射率</el-radio>
                </div>
                <div class="formaction" style="display: flex;margin: 0 1vw;padding: 0;justify-content: space-around;width: 90%;">
                  <div class="button" style="margin-left: -1vw;" >加载</div>
                  <div class="button" >保存</div>
                </div>
                <div class="formaction" style="padding-right: 3.5vw;padding-left: 2.5vw;width: 12vw;">
                  <div class="text">范围（km）</div>
                  剖面
                </div>
                <div class="formaction" style="padding: 0 3.7vw 0 3.1vw;width: 11vw">
                  <div>
                    <el-input   v-model="Range" autocomplete="off" @focus="onFocus" @blur="onBlur" :disabled="this.refractivity_type !== 'Range-dep.refractivity'"
                      style="width: 3.7vw;margin-left: -0.5vw;"></el-input>
                  </div>
                  <div style="width: 5.5vw;text-align: left;color: #fff;" @click="refractivity_type === 'Range-dep.refractivity'?showAtmosphereOptionP():null" @focus="onFocus"
                    @blur="onBlur" tabindex="0">
                    <div class="xialakuang" style="width: 5vw;margin-left: 2.5vw;">
                      <img :src="require('@/assets/img/graphInput.png')"
                        style="position: absolute;z-index: 99;width:28%;height: 80%;">
                      <div class="selected-option" style="margin-left: 0.5vw">
                        {{ getLabel(Profile, atmosphereTypeList) || '' }}
                      </div>
                      <img :src="require('@/assets/img/graphDown.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2.5vw;top: 0;"
                        v-if="typePic3 == 0">
                      <img :src="require('@/assets/img/graphUp.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 2.5vw;top: 0;"
                        v-if="typePic3 == 1">
                    </div>
                  </div>
                  <ul v-if="atmosphereOptionP" class="options" style="width: 4vw;right: 2vw;">
                    <li v-for="(item, index) in atmosphereTypeList" :key="index" @click="selectAtmosphereOptionP(item)">
                      {{ item.label }}
                    </li>
                  </ul>
                </div>
                <div class="atmosphere-table">
                  <table>
                    <tbody>
                      <tr v-for="(item, index) in atmosphereTable" :key="index">
                        <td><el-input type="text" v-model="item.range" :disabled="refractivity_type !== 'Range-dep.refractivity'" /></td>
                        <td><el-input type="text" v-model="item.profile" class="inputTz" style="width: 9vw;" :disabled="refractivity_type !== 'Range-dep.refractivity'" /></td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>

          <!--中间三个-->
          <div style="display: flex;flex-direction: column;width: 19vw;margin-right: 0.7vw;">
            <div class="back">
              <div class="biaotou">
                <div class="biaotou-left">分析参数</div>
              </div>
              <div>
                <div class="formaction1">
                  <el-radio v-model="analysis_type" label="One-way">单向</el-radio>
                  <el-radio v-model="analysis_type" label="Two-way">双向</el-radio>
                </div>
                <div class="formaction">
                  距离步长(m)
                  <el-input  style="margin-right: 1vw;" v-model="range_step" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
                <div class="formaction">
                  高度步长 (m)
                  <el-input  style="margin-right: 1vw;" v-model="altitude_step" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div>
            </div>
            <div class="back">
              <div class="biaotou">
                <div class="biaotou-left">介质表面参数</div>
              </div>
              <div class="formaction">
                <el-radio v-model="surface_type" label="Impedance surface" auto-width="true">阻抗表面</el-radio>
                <el-radio v-model="surface_type" label="Perfectly conducting" auto-width="true">理想导体</el-radio>
              </div>
              <div class="formaction">
                类型
                <div class="selectInfo1"  @click="showSurfaceOption" @focus="onFocus"
                  @blur="onBlur" tabindex="0">
                  <div class="xialakuang" style="margin-left: -1vw;">
                    <div class="selected-option">
                      <img :src="require('@/assets/img/graphInput.png')"
                        style="position: absolute;z-index: 99;width:33%;height: 80%;">
                      <div class="selected-option" style="margin-left: 0.5vw">
                        {{ getLabel(surface_type_combobox, surfaceTypeList) || '' }}
                      </div>
                      <img :src="require('@/assets/img/graphDown.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 0.8vw;top: 0;"
                        v-if="typePic4 == 0">
                      <img :src="require('@/assets/img/graphUp.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 0.8vw;top: 0;"
                        v-if="typePic4 == 1">
                    </div>
                  </div>
                </div>
                <ul v-if="surfaceOption" class="options" style="right: 0.8vw;width:5vw">
                  <li v-for="(item, index) in surfaceTypeList" :key="index" @click="selectSurfaceOption(item)">
                    {{ item.label }}
                  </li>
                </ul>
              </div>
              <div class="formaction">
                介电常数
                <el-input style="margin-right: 1vw;" v-model="dielectric_constant" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
              <div class="formaction">
                电导率 (s/m)
                <el-input style="margin-right: 1vw;" v-model="conductivity" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
              </div>
            </div>
            <div class="back" style="height: 40vh;">
              <div class="biaotou">
                <div class="biaotou-left">地形参数</div>
              </div>
              <div>
                <div class="formaction1">
                  <el-radio v-model="terrain_type" label="None (Flat)" style="margin-left: 0.8vw;">无（平坦地形）</el-radio>
                  <el-radio v-model="terrain_type" label="Terrain" style="margin-left: 2.5vw;">地形</el-radio>
                </div>
                <div class="formaction" style="width: 82%;">
                  <div style="margin-left: 0.5vw;">插值类型</div>
                  <div class="selectInfo1" @click="showTerrainOption" @focus="onFocus"
                    @blur="onBlur" tabindex="0">
                    <div class="xialakuang">
                      <img :src="require('@/assets/img/graphInput.png')"
                        style="position: absolute;z-index: 99;width:23%;height: 80%;">
                      <div class="selected-option">
                        {{ getLabel(interpolation_type, terrainInterpolationList) || '' }}
                      </div>
                      <img :src="require('@/assets/img/graphDown.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 1.5vw;top: 0;"
                        v-if="typePic5 == 0">
                      <img :src="require('@/assets/img/graphUp.png')"
                        style="position: absolute;z-index: 99;width: 3%;height: 100%;object-fit: contain;right: 1.5vw;top: 0;"
                        v-if="typePic5 == 1">
                    </div>
                  </div>
                  <ul v-if="terrainOption" class="options">
                    <li v-for="(item, index) in terrainInterpolationList" :key="index"
                      @click="selectTerrainOption(item)">
                      {{ item.label }}
                    </li>
                  </ul>
                </div>
                <div class="formaction" style="width: 80%;">
                  <div class="text" style="margin-left: 1.6vw;">点数</div>
                  <div>
                    <el-input  style="margin-right: 1vw;" v-model="num_points" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="formaction" style="display: flex;margin: 0 2vw;padding: 0;justify-content: space-between;width: 78%;">
                  <!-- <div class="button">定位点</div> -->
                  <div class="button" @click="initChart" style="margin-left: 1vw;">绘图</div>
                  <div class="button">清除</div>
                </div>
                <!-- <div class="formaction" style="display: flex;margin: 0 2vw;padding: 0;justify-content: space-between">
                  <div class="button">加载</div>
                  <div class="button">保存</div>
                  
                </div> -->
                <div class="formaction"  style="width: 78%;">
                  <div class="text" style="margin-left: 0.5vw;">范围（km）</div>
                  <div class="text">高度（m）</div>
                </div>
                <div class="formaction" style="width: 88%;">
                  <div>
                    <el-input  style="margin-right: 1vw;margin-left: 0.6vw;" v-model="tRange" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                  <div>
                    <el-input   style="margin-right: 2.5vw;" v-model="Height" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
                  </div>
                </div>
                <div class="terrain-table">
                  <table>
                    <tbody>
                      <tr v-for="(item, index) in terrainTable" :key="index">
                        <td><el-input type="text" v-model="item.range" /></td>
                        <td><el-input type="text" v-model="item.height" /></td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>

          <!--右边上下2个-->
          <div style="display: flex;flex-direction: column;width: 39vw;">
            <!--上方图片留白2个-->
            <div>
              <div style="display: flex;margin-bottom: 1vh;padding-left: -1vw;">
                <div class="picture-container" style="display: flex;justify-content: center;">
                  <!-- <img :src="src1" style="width:100%;height: 100%;justify-items: center;" v-if="src1 != ''" @click="showBigInfo(src1)" /> -->
                   <div id="terrainChart" style="width: 100%;height: 30vh;margin-left: -3vw;"></div>
                </div>
              </div>
              <div class="loader" v-if="showJZ"></div>
              <div style="display: flex;margin-bottom: 1vh;justify-content: center">
                <div class="picture-container" style="display: flex; justify-content: center; width: 100%;background-color: #FFFFFF;border: 2px solid  #006cda;">
                  <div id="heatmap-chart" style="width: 100%; height: 16vw;position: relative; top: -30px;"></div>
<!--                  <img :src="src2" style="width:100%;height: 100%;justify-items: center;" v-if="src2 != ''" @click="showBigInfo(src2)" />-->
                </div>
              </div>
            </div>
            <!-- 下方模块 -->
            <div style="display:inline-flex; width: 100%;height:21%;justify-content: space-between;">
              <div class="backC">
                <div class="biaotouC">
                  <div class="biaotou-left">绘图类型</div>
                </div>
                <div>
                  <div class="formactionC">
                    <el-radio v-model="plotType" label="1">传播因子
                    </el-radio>
                  </div>
                  <div class="formactionC">
                    <el-radio v-model="plotType" label="2">路径损耗
                    </el-radio>
                  </div>
                </div>
              </div>
              <div class="backC">
                <div class="biaotouC">
                  <div class="biaotou-left">当前点</div>
                </div>
                <div class="formactionC">
                  <div class="text">范围(km)</div>
                  <div style="min-width:4vw; text-align:center;height: 100%;" class="inputbg">{{ CPRange }}</div>
                </div>
                <div class="formactionC">
                  <div class="text">高度(m)</div>
                  <div style="min-width:4vw;text-align:center;height: 100%;" class="inputbg">{{ CPAltitude }}</div>
                </div>
                <div class="formactionC">
                  <div class="text">值(dB)</div>
                  <div style="min-width:4vw;text-align:center;height: 100%;" class="inputbg">{{ CPvalue }}</div>
                </div>
              </div>
              <!-- <div class="backC">
                <div class="biaotouC">
                  <div class="biaotou-left">二维图形</div>
                </div>
                <div class="formactionC">
                  范围 (km)
                  <el-input v-model="TDGraphRange" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
                <div class="formactionC">
                  高度 (m)
                  <el-input v-model="TDGraphAltitude" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div> -->
              <div class="backC" style="height: 73%;">
                <div class="biaotouC">
                  <div class="biaotou-left">颜色条</div>
                </div>
                <div class="formactionC">
                  最小值:
                  <el-input v-model="colorbarMin" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
                <div class="formactionC">
                  最大值:
                  <el-input v-model="colorbarMax" @focus="onFocus" @blur="onBlur"></el-input>
                </div>
              </div>
              
            </div>
            <el-button type="primary" class="buttonRun" @click="LDWLT()">运行</el-button>



          </div>
        </div>
      </div>

      <el-dialog title="预览" :visible.sync="showBig">
        <div style="height: 20vw;width: 20vw;margin: 0 auto">
          <img :src="bigUrl" style="height: 100%;object-fit: contain;">
        </div>

      </el-dialog>

      <!--      弹窗一-->
      <el-dialog :visible.sync="dialogSAPVisible" class="showInfo1">
        <div style="display: flex; flex-direction: row">
          <div style="color: #fff; background-color: #004e9c;border-radius: 20px;width: 10vw; height: 3.7vh;align-items: center;justify-content: center; font-size: 20px;margin-top: -2%">
            <div style="margin-left: 20%;margin-top: 2%;width: 100%;">
              标准大气
            </div>
          </div>
          <el-button size="small" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #f19149;color: #FFFFFF;margin-top: -1%; margin-left: 50%" @click="DQ2">绘图</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">确定</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">取消</el-button>
          <el-button size="small" @click="save2" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">保存</el-button>
        </div>
        <div style="display: flex; flex-direction: row;width: 100%;height: 100%; margin-top: 4%">
          <div style="margin-left: 2vw;width: 30%">
            <el-form :model="form1" style="width: 100%">
              <div>
                <div style="color: black">范围(km)</div>
                <input v-model="form1.Range" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 4vh"
                class="doubleForm">
                <div style="color: black;margin-left: 30%">M</div>
                <div style="color: black;margin-right: 10%">高度(m)</div>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;">
                <div style="color: black">M0</div>
                <input v-model="form1.M_entry" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z0</div>
                <input v-model="form1.altitude_entry" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>

            </el-form>

          </div>
          <div style="margin-left: 2vw;width: 60%">
            <img :src="src3" style="width:100%;object-fit: contain; " />
          </div>
        </div >
      </el-dialog>
      <el-dialog :visible.sync="dialogSDVisible" class="showInfo1">
        <div style="display: flex; flex-direction: row">
          <div style="color: #fff; background-color: #004e9c;border-radius: 20px;width: 10vw; height: 3.7vh;align-items: center;justify-content: center; font-size: 20px;margin-top: -2%">
            <div style="margin-left: 20%;margin-top: 2%;width: 100%;">
              表面波导
            </div>
          </div>
          <el-button size="small" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #f19149;color: #FFFFFF;margin-top: -1%; margin-left: 50%" @click="DQ2">绘图</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">确定</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">取消</el-button>
          <el-button size="small" @click="save2" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">保存</el-button>
        </div>
        <div style="display: flex; flex-direction: row; margin-top: 4%">
          <div style="margin-left: 2vw;width: 30%">
            <el-form :model="form2" style="width: 100%">

              <div>
                <div style="color: black">范围(km)</div>
                <input v-model="form2.Range" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="margin-top: 3vh">
                <div style="color: black">M</div>
                <input v-model="form2.name" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M0</div>
                <input v-model="form2.S_M_entry" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z0</div>
                <input v-model="form2.s_altitude_entry" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M1</div>
                <input v-model="form2.S_M_entry1" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z1</div>
                <input v-model="form2.s_altitude_entry1" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M2</div>
                <input v-model="form2.S_M_entry2" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z2</div>
                <input v-model="form2.s_altitude_entry2" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>

            </el-form>
            <div style="display: flex;justify-content: center;">

            </div>
            <div style="display: flex;justify-content: center;">
              <div slot="footer"
                style="margin-top: 2vh;display: flex;justify-content: space-between;align-items: center;width: 9vw;">

              </div>
            </div>
          </div>
          <div style="margin-left: 2vw;width: 60%">
            <img :src="src4" style="width:100%;object-fit: contain; " />
          </div>
        </div>
      </el-dialog>
      <el-dialog :visible.sync="dialogSBDVisible" class="showInfo1">
        <div style="display: flex; flex-direction: row">
          <div style="color: #fff; background-color: #004e9c;border-radius: 20px;width: 10vw; height: 3.7vh;align-items: center;justify-content: center; font-size: 20px;margin-top: -2%">
            <div style="margin-left: 20%;margin-top: 2%;width: 100%;">
              基于表面
            </div>
          </div>
          <el-button size="small" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #f19149;color: #FFFFFF;margin-top: -1%; margin-left: 50%" @click="DQ2">绘图</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">确定</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">取消</el-button>
          <el-button size="small" @click="save2" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">保存</el-button>
        </div>
        <div style="display: flex; flex-direction: row;margin-top: 4%">
          <div style="margin-left: 2vw;width: 30%">
            <el-form :model="form3" style="width: 100%">

              <div>
                <div style="color: black">范围(km)</div>
                <input v-model="form3.Range" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="margin-top: 3vh">
                <div style="color: black">M</div>
                <input v-model="form3.name" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M0</div>
                <input v-model="form3.S_M_entry" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z0</div>
                <input v-model="form3.s_altitude_entry" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M1</div>
                <input v-model="form3.S_M_entry1" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z1</div>
                <input v-model="form3.s_altitude_entry1" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M2</div>
                <input v-model="form3.S_M_entry2" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z2</div>
                <input v-model="form3.s_altitude_entry2" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M3</div>
                <input v-model="form3.S_M_entry3" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z3</div>
                <input v-model="form3.s_altitude_entry3" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>

            </el-form>
          </div>
          <div style="margin-left: 2vw;width: 60%">
            <img :src="src5" style="width:100%;object-fit: contain; " />
          </div>
        </div>
      </el-dialog>
      <el-dialog title="悬空波导" :visible.sync="dialogEDVisible" class="showInfo1">
        <div style="display: flex; flex-direction: row">
          <div style="color: #fff; background-color: #004e9c;border-radius: 20px;width: 10vw; height: 3.7vh;align-items: center;justify-content: center; font-size: 20px;margin-top: -2%">
            <div style="margin-left: 20%;margin-top: 2%;width: 100%;">
              悬空波导
            </div>
          </div>
          <el-button size="small" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #f19149;color: #FFFFFF;margin-top: -1%; margin-left: 50%" @click="DQ2">绘图</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">确定</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">取消</el-button>
          <el-button size="small" @click="save2" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">保存</el-button>
        </div>
        <div style="display: flex; flex-direction: row;margin-top: 4%">
          <div style="margin-left: 2vw;width: 30%">
            <el-form :model="form4" style="width: 100%">

              <div>
                <div style="color: black">范围(km)</div>
                <input v-model="form4.Range" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="margin-top: 3vh">
                <div style="color: black">M</div>
                <input v-model="form4.name" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M0</div>
                <input v-model="form4.e_M_entry" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z0</div>
                <input v-model="form4.e_altitude_entry" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M1</div>
                <input v-model="form4.e_M_entry1" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z1</div>
                <input v-model="form4.e_altitude_entry1" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M2</div>
                <input v-model="form4.e_M_entry2" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z2</div>
                <input v-model="form4.e_altitude_entry2" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                <div style="color: black">M3</div>
                <input v-model="form4.e_M_entry3" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <div style="color: black">Z3</div>
                <input v-model="form4.e_altitude_entry3" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>

            </el-form>
          </div>
          <div style="margin-left: 2vw;width: 60%">
            <img :src="src6" style="width:100%;object-fit: contain; " />
          </div>
        </div>
      </el-dialog>
      <el-dialog title="蒸发波导" top="20px" :visible.sync="dialogEvaDVisible" width="70%" class="showInfo1">
        <div style="display: flex; flex-direction: row;margin-left: 5%">
          <div style="color: #fff; background-color: #004e9c;border-radius: 20px;width: 7vw; height: 3.7vh;align-items: center;justify-content: center; font-size: 20px;margin-top: -2%">
            <div style="margin-left: 20%;margin-top: 2%">
              蒸发波导
            </div>
          </div>
          <el-button size="small" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #f19149;color: #FFFFFF;margin-top: -1%; margin-left: 65%" @click="DQ2">绘图</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">确定</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">取消</el-button>
          <el-button size="small" @click="save2" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">保存</el-button>
        </div>
        <div style="display: flex; flex-direction: row;margin-left: 5%;margin-top: 4%">
          <div style="display: flex; flex-direction: column; width: 35%">
            <div style="margin-left: 2vw;width: 80%">
              <img :src="src7" style="width:100%;object-fit: contain; " />
            </div>
            <div style="display: flex;flex-direction: column; width: 100%;justify-content: start;margin-top: 4%;">
              <div style="color: black;font-size: 20px">创建波导剖面</div>
              <el-form :model="form5" style="margin-top: 1vh">
                <el-form-item style="text-align: left;">
                  <el-select v-model="form5.typeLeft" style="width: 14vw; height: 3vh;">
                    <el-option label="手动定义波导高度" value="Define Duct Height Manually"></el-option>
                    <el-option label="使用蒸发波导模型" value="Use Evaporation Duct Model"></el-option>
                  </el-select>
                </el-form-item>
                <div>
                  <div style="color: black">范围(km)</div>
                  <input v-model="form5.max_altitude" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                </div>
              </el-form>
              <div style="color: black;margin-top: 4vh;font-size: 20px">手动定义波导</div>
              <el-form :model="form5" style="margin-top: 1vh">
                <div style="margin-top: 3vh">
                  <div style="color: black">波导高度(m)</div>
                  <input disabled v-model="form5.max_altitude" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                </div>
                <div style="margin-top: 3vh">
                  <div style="color: black">M0</div>
                  <input disabled v-model="form5.max_altitude" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                </div>
              </el-form>
            </div>

          </div>
          <div style="width: 60%">
            <el-card style="background-color: #006cda; border-radius: 20px;">
              <div style="color: #004e9c; background-color: #fff;border-radius: 20px;width: 14vw; height: 3.7vh;align-items: center;justify-content: center; font-size: 20px;margin-top: 0%">
                <div style="margin-left: 20%;margin-top: 2%">
                  使用蒸发波导模型
                </div>
              </div>
              <div style="margin-top: 2vh">

                <el-form :model="form5">
                  <div style="margin-left: 50%; color: #FFFFFF; font-size: 18px">选择波导模型</div>
                  <el-form-item style="margin-top: 1vh">
                    <el-col :span="11">
                      <el-select v-model="form5.region" style="border:1px solid">
                        <el-option label="手动定义Atm数据" value="Define Atm.Data Manually"></el-option>
                        <el-option label="从文件加载Atm数据" value="Load Atm.Data From File"></el-option>
                      </el-select>
                    </el-col>
                    <el-col :span="11">
                      <el-form-item>
                        <el-select v-model="form5.typeRight" style="border:1px solid">
                          <el-option label="Beljaars-Holtslag" value="Beljaars-Holtslag"></el-option>
                          <el-option label="Businger-Dyer" value="Businger-Dyer"></el-option>
                          <el-option label="BYC" value="BYC"></el-option>
                          <el-option label="Cheng-Brutsaert" value="Cheng-Brutsaert"></el-option>
                          <el-option label="LKB" value="LKB"></el-option>
                          <el-option label="NPS" value="NPS"></el-option>
                          <el-option label="NRL" value="NRL"></el-option>
                          <el-option label="NWA" value="NWA"></el-option>
                          <el-option label="RSHMU" value="RSHMU"></el-option>
                          <el-option label="SHEBA" value="SHEBA"></el-option>
                          <el-option label="Toga-Coare" value="Toga-Coare"></el-option>
                          <el-option label="Paulys_Jeske" value="Paulys_Jeske"></el-option>
                        </el-select>
                      </el-form-item>
                    </el-col>
                  </el-form-item>
                  <el-form-item>
                    <div style="color: #FFFFFF; font-size: 18px">大气数据</div>
                    <div style="border-top: black 1px solid;margin-top: -4vh; display: flex; flex-direction: row">
                      <el-form :model="form5" style="margin-top: 1vh; width: 90%">
                        <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                          <div style="display: flex;flex-direction: row;width: 50% ">
                            <div style="color: #fff;width:8vw;">大气温度</div>
                            <input v-model="form5.atmosferikSicaklik" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">C</div>
                          </div>
                          <div style="display: flex;flex-direction: row;width: 50% ;margin-left: 4vw">
                            <div style="color: #fff;width:8vw;">海洋表面温度</div>
                            <input v-model="form5.denizYuzeySicakligi" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">C</div>
                          </div>
                        </div>
                        <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                          <div style="display: flex;flex-direction: row;width: 50% ">
                            <div style="color: #fff;width:8vw;">大气压缩</div>
                            <input v-model="form5.atmosferikSicaklik" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">mbar</div>
                          </div>
                          <div style="display: flex;flex-direction: row;width: 50% ;margin-left: 4vw">
                            <div style="color: #fff;width:8vw;">相对温度</div>
                            <input v-model="form5.denizYuzeySicakligi" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">%</div>
                          </div>
                        </div>
                        <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                          <div style="display: flex;flex-direction: row;width: 50% ">
                            <div style="color: #fff;width:8vw;">比湿度</div>
                            <input v-model="form5.atmosferikSicaklik" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">kg/kg</div>
                          </div>
                          <div style="display: flex;flex-direction: row;width: 50% ;margin-left: 4vw">
                            <div style="color: #fff;width:8vw;">初始潜在温度</div>
                            <input v-model="form5.denizYuzeySicakligi" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">K</div>
                          </div>
                        </div>
                        <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                          <div style="display: flex;flex-direction: row;width: 50% ">
                            <div style="color: #fff;width:8vw;">风速</div>
                            <input v-model="form5.atmosferikSicaklik" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">m/s</div>
                          </div>
                          <div style="display: flex;flex-direction: row;width: 50% ;margin-left: 4vw">
                            <div style="color: #fff;width:8vw;">蒸汽压缩</div>
                            <input v-model="form5.denizYuzeySicakligi" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">Pa</div>
                          </div>
                        </div>
                        <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                          <div style="display: flex;flex-direction: row;width: 50%  ">
                            <div style="color: #fff;width:8vw;">平均表层温度</div>
                            <input v-model="form5.atmosferikSicaklik" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">K</div>
                          </div>
                          <div style="display: flex;flex-direction: row;width: 50% ;margin-left: 4vw">
                            <div style="color: #fff;width:8vw;">风速测量高度</div>
                            <input v-model="form5.denizYuzeySicakligi" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">m</div>
                          </div>
                        </div>
                        <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 3vh">
                          <div style="display: flex;flex-direction: row;width: 50% ">
                            <div style="color: #fff;width:8vw;">大气温度测量高度</div>
                            <input v-model="form5.atmosferikSicaklik" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">m</div>
                          </div>
                          <div style="display: flex;flex-direction: row;width: 50%;margin-left: 4vw">
                            <div style="color: #fff;width:8vw;">相对温度测量高度</div>
                            <input v-model="form5.denizYuzeySicakligi" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                            <div style="color: #fff;margin-left: 1vw;width:3vw">m</div>
                          </div>
                        </div>
                      </el-form>
                    </div>

                  </el-form-item>

                </el-form>
              </div>
            </el-card>



          </div>
        </div>


      </el-dialog>
      <el-dialog title="用户自定义" :visible.sync="dialogUDVisible" class="showInfo1">
        <div style="display: flex; flex-direction: row">
          <div style="color: #fff; background-color: #004e9c;border-radius: 20px;width: 10vw; height: 3.7vh;align-items: center;justify-content: center; font-size: 20px;margin-top: -2%">
            <div style="margin-left: 20%;margin-top: 2%;width: 100%;">
              用户自定义
            </div>
          </div>
          <el-button size="small" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #f19149;color: #FFFFFF;margin-top: -1%; margin-left: 50%" @click="DQ2">绘图</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">确定</el-button>
          <el-button size="small" @click="dialogSDVisible = false"
                     style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">取消</el-button>
          <el-button size="small" @click="save2" style="width: 3vw;height:3vh;display: flex;justify-content: center;background-color: #004e9c;color: #FFFFFF;margin-top: -1%">保存</el-button>
        </div>
        <div style="display: flex; flex-direction: row;height: 30vw; margin-top: 4%">
          <div style="margin-left: 2vw;width: 30%">
            <el-form :model="form6" style="width: 100%">
              <div>
                <div style="color: black">范围(km)</div>
                <input v-model="form6.name" style="width: 14vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;margin-top: 4vh"
                   class="doubleForm">
                <div style="color: black;margin-left: 20%">M</div>
                <div style="color: black;margin-right: 10%">高度(m)</div>
              </div>
              <div style="display: flex;flex-direction: row;justify-content: space-between;align-items: center;">
                <input v-model="form6.M_units[form6.M_units.length - 1]" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
                <input v-model="form6.altitude[form6.altitude.length - 1]" style="width: 5vw; border:2px #004e9c solid; border-radius: 20px; height: 3vh;margin-top: 1vh"/>
              </div>

            </el-form>
<!--            <el-form :model="form6" style="width: 100%">-->
<!--              <el-form-item label="范围(km)">-->
<!--                <el-input v-model="form6.name" style="width: 8vw; border:1px solid; border-radius: 5%"></el-input>-->
<!--              </el-form-item>-->
<!--              <el-form-item>-->
<!--                <el-col :span="9.75">-->
<!--                  <el-form-item size="small" label="M">-->
<!--                    <el-input v-model="form6.M_units[form6.M_units.length - 1]"-->
<!--                      style="width: 8vw; border:1px solid; border-radius: 5%"></el-input>-->
<!--                  </el-form-item>-->
<!--                </el-col>-->
<!--                <el-col :span="11" style="margin-left: 2vw">-->
<!--                  <el-form-item size="small" label="高度(m)">-->
<!--                    <el-input v-model="form6.altitude[form6.altitude.length - 1]"-->
<!--                      style="width: 8vw; border:1px solid; border-radius: 5%"></el-input>-->
<!--                  </el-form-item>-->
<!--                </el-col>-->
<!--              </el-form-item>-->
<!--            </el-form>-->
            <div style="width: 100%;height: 20%;display: flex;flex-direction: row;justify-content: space-around;border: 1px solid #006cda;border-radius: 20px; margin-top: 2vh">
              <div style="width: 50%;height:100%;">
                <div style="text-align: center;font-size: 1vw;" v-for="(item, index) in list" :key="item"
                  @click="DQ6info(index)">{{ item[0] }}</div>
              </div>
              <div style="width: 50%;height:100%;">
                <div style="text-align: center;font-size: 1vw;" v-for="(item, index) in list" :key="item"
                  @click="DQ6info(index)">{{ item[1] }}</div>
              </div>
            </div>



          </div>
          <div style="margin-left: 2vw;width: 60%">
            <img :src="src8" style="width:100%;object-fit: contain; " />
          </div>
        </div>
      </el-dialog>
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  data() {
    return {
      showBig:false,
      bigUrl:"",

      // 弹窗Visible
      dialogSAPVisible: false,
      typePic1: false,
      typePic2: false,
      typePic3: false,
      typePic4: false,
      typePic5: false,
      form1: {
        M_entry: 300.0,
        altitude_entry: 0.0,
        Range: "",
        name: ""
      },
      form: {
        name: "11111"
      },


      dialogSDVisible: false,
      form2: {
        S_M_entry: 350.0,
        s_altitude_entry: 0.0,
        S_M_entry1: 300.0,
        s_altitude_entry1: 100.0,
        S_M_entry2: 350.0,
        s_altitude_entry2: 300.0,
        Range: "",
        name: ""
      },


      dialogSBDVisible: false,
      form3: {
        S_M_entry: 340.0,
        s_altitude_entry: 0.0,
        S_M_entry1: 356.0,
        s_altitude_entry1: 135.0,
        S_M_entry2: 340.0,
        s_altitude_entry2: 150.0,
        S_M_entry3: 358.0,
        s_altitude_entry3: 300.0,
        Range: "",
        name: ""
      },
      dialogEDVisible: false,
      form4: {
        e_M_entry: 300.0,
        e_altitude_entry: 0.0,
        e_M_entry1: 330.0,
        e_altitude_entry1: 100.0,
        e_M_entry2: 310.0,
        e_altitude_entry2: 150.0,
        e_M_entry3: 350.0,
        e_altitude_entry3: 300.0,
        Range: "",
        name: ""
      },
      form5: {
        typeRight: "Toga-Coare",
        typeLeft: "Define Duct Height Manually",
        max_altitude: 1000.0,
        atmosferikSicaklik: 24,
        denizYuzeySicakligi: 14.85,
        atmosferikBasinc: 1011.9,
        bagilNem: 40,
        spesifikNem: 0.02,
        baslangicPotansiyelSicakligi: 310,
        ruzgarHizi: 10,
        ruzgarHiziOlcumYuksekligi: 1,
        havaSicakligiOlcumYuksekligi: 11,
        bagilNemOlcumYuksekligi: 1,
        ortalamaYuzeyKatmanSicakligi: 289.95,
        suBuhariBasinci: 3040,
      },

      dialogEvaDVisible: false,
      dialogUDVisible: false,
      form6: {
        M_units: [300.0],
        altitude: [0.0],
        Range: "",
        name: ""
      },
      list: [[450, 0], [250, 100], [300, 250]],



      maxRange: 150.0,
      maxAltitude: 1900.0,
      range_step: 200.0,
      altitude_step: 0.29,
      analysis_type: "One-way",
      polarization: "Horizontal",
      Horizontal: 2.0,
      beamwidth: 1.0,
      elevation_angle: 0.0,
      antenna_height: 1052,
      frequency: 3000,

      surface_type: 'Perfectly conducting',
      surface_type_combobox: 'Sea',
      dielectric_constant: 15,
      conductivity: 0.22934,
      refractivity_type: 'Range-indep. refractivity',
      refractivity_type_combobox: 'Evaporation duct',
      Range: 0.0,
      Profile: "Standard atmosphere",
      terrain_type: 'Terrain',
      interpolation_type: 'Linear',
      num_points: 2.0,
      tRange: 0.0,
      Height: 1051.0,


      src1: "",
      src2: "",
      src3: require("@/assets/img/tc1.png"),
      src4: require("@/assets/img/tc2.png"),
      src5: require("@/assets/img/tc3.png"),
      src6: require("@/assets/img/tc4.png"),
      src7: require("@/assets/img/tc5.png"),
      src8: require("@/assets/img/tc6.png"),
      CPRange: '0',
      showJZ: false,
      dataFinal1: {
        jsId: null,
        jsResult: {},
        allImg: null,
      },
      CPAltitude: '0',
      CPvalue: '0',
      TDGraphRange: '0',
      TDGraphAltitude: '0',
      colorbarMin: '0',
      colorbarMax: '0',
      plotType: '1',

      polarizationList: [
        { value: 'Vertical', label: '纵向' },
        { value: 'Horizontal', label: '横向' },
      ],
      atmosphereTypeList: [
        { value: 'Standard atmosphere', label: '标准大气' },
        { value: 'Surface duct', label: '表面波导' },
        { value: 'Surface-based', label: '基于表面' },
        { value: 'Elevated duct', label: '悬空波导' },
        { value: 'Evaporation duct', label: '蒸发波导' },
        { value: 'User defined', label: '用户自定义' },
      ],
      atmosphereOption: false,
      atmosphereTable: [
        { range: '0', profile: '标准大气' },
        { range: '5', profile: '表面波导' },
        { range: '10', profile: '悬空波导' },
        { range: '25', profile: '蒸发波导' },
        { range: '50', profile: '用户自定义' },
      ],
      lasted: "",
      atmosphereOptionP: false,

      surfaceTypeList: [
        { value: 'Sea', label: '海水' },
        { value: 'Fresh water', label: '淡水' },
        { value: 'Wet ground', label: '潮湿地面' },
        { value: 'Medium dry ground', label: '中等干燥地面' },
        { value: 'very dry ground', label: '极干燥地面' },
        { value: 'User defined', label: '用户自定义' },
      ],
      surfaceOption: false,

      terrainInterpolationList: [
        { value: 'None', label: '无' },
        { value: 'Linear', label: '线性' },
        { value: 'Cubicsplice', label: '立方' },
      ],
      terrainOption: false,

      terrainTable: [
        { range: 0, height: 1051.0 },
        { range: 0.8333333, height: 1080.6776 },
        { range: 1.666667, height: 1068.8258 },
        { range: 2.5, height: 1021.7262 },
        { range: 3.333333, height: 1016.1403 },
      ],

      showOption: false,


      //新的
      chart: null,
      loading: false,
      error: '',
      heatmapData: null,
      metadata: null,
      currentHoverData:null
    };
  },
  watch: {
    // 监听 plotType 的变化
    plotType(newVal, oldVal) {
      // 避免第一次初始化时也触发
      if (newVal === oldVal) return;

      // 根据新的值调用不同的方法
      if (newVal === '1') {
        this.propagation();
      } else if (newVal === '2') {
        this.pathLoss();
      }
    }
  },
  methods: {
    async initChart() {
      await this.$nextTick()
      const chart = echarts.init(document.getElementById('terrainChart'));
      const res = await this.DXT();
      const data = res.data;
      const originalPoints = data.original_points || [];
      // const processedPoints = data.processed_points || [];
      const interpolatedPoints = data.interpolated_points || [];
      
      // 创建系列数据
      const series = [];
      
      // 添加原始点系列
      if (originalPoints.length > 0) {
        series.push({
          name: '原始点',
          type: 'scatter',
          data: originalPoints,
          symbolSize: 5,
          itemStyle: { color: '#000000' }
        });
      }

      // 添加插值地形系列
      if (interpolatedPoints.length > 0) {
        series.push({
          name: '插值地形',
          type: 'line',
          data: interpolatedPoints,
          smooth: data.interpolation_type === 'CubicSpline',
          symbol: 'none',
          lineStyle: { width: 2, color: '#00CC7A' },
          areaStyle: {
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
              { offset: 0, color: 'rgba(0, 204, 122)' },
              { offset: 1, color: 'rgba(0, 204, 122)' }
            ])
          }
        });
      }

      // 图表配置
      const option = {
        title: {
          text: `地形`,
          textStyle: {
            color: '#ffffff'   // 文字颜色
          }
        },
        tooltip: {
          trigger: 'axis',
          formatter: params => {
            return params.map(param => 
              `${param.seriesName}: (${param.value[0]} km, ${param.value[1]} m)`
            ).join('<br/>');
          }
        },
        legend: {
          data: series.map(item => item.name),
          right: '10%',     // 距离右侧10%
          top: '5%',        // 距离顶部5%
          orient: 'horizontal', // 水平排列
          textStyle: {
            color: '#ffffff'   // 文字颜色
          }
        },
        xAxis: {
          type: 'value',
          name: '距离 (km)',
          min: 0,
          interval: 50,
          max: data.rangekm || 100,
          nameTextStyle: {
            color: '#fff'  // x轴名称颜色改为白色
          },
          axisLabel: {
            color: '#fff'  // x轴刻度标签颜色改为白色
          },
          axisLine: {
            lineStyle: {
              color: '#fff'  // x轴线颜色改为白色
            }
          },
          axisTick: {
            lineStyle: {
              color: '#fff'  // x轴刻度颜色改为白色
            }
          },
          splitLine: {
            show: false  // 去掉x轴方向的网格线
          }

        },
        yAxis: {
          type: 'value',
          name: '高度 (m)',
          min: 0,
          interval: 380,
          max: data.hmax || 1000,
          nameTextStyle: {
            color: '#fff'  // y轴名称颜色改为白色
          },
          axisLabel: {
            color: '#fff'  // y轴刻度标签颜色改为白色
          },
          axisLine: {
            lineStyle: {
              color: '#fff'  // y轴线颜色改为白色
            }
          },
          axisTick: {
            lineStyle: {
              color: '#fff'  // y轴刻度颜色改为白色
            }
          },
          splitLine: {
            show: false  // 去掉x轴方向的网格线
          }
        },
        series: series
      };
      

      chart.setOption(option);
    },





    //echarts下边的图
    // 初始化图表
    initChartDown() {
      const chartDom = document.getElementById('heatmap-chart')
      this.chart = echarts.init(chartDom)

      // 窗口大小变化时重绘图表
      window.addEventListener('resize', () => {
        if (this.chart) {
          this.chart.resize()
        }
      this.chart.resize()
      })
    },
    // 渲染图表
    // 渲染图表
    // 渲染图表
    // 数据聚合方法
    // 主渲染入口
    aggregateHeatmapData(data, xAxis, yAxis) {
      const aggregated = new Map();
      const dataLength = data.length;

      for (let i = 0; i < dataLength; i++) {
        const item = data[i];
        const xIndex = item[0];
        const yIndex = item[1];
        const value = item[2];

        const key = (xIndex << 16) | yIndex;

        if (!aggregated.has(key)) {
          aggregated.set(key, { sum: value, count: 1 });
        } else {
          const aggItem = aggregated.get(key);
          aggItem.sum += value;
          aggItem.count += 1;
        }
      }

      const result = new Array(aggregated.size);
      let index = 0;

      for (const [key, value] of aggregated) {
        const xIndex = (key >> 16) & 0xFFFF;
        const yIndex = key & 0xFFFF;
        // 对聚合后的值进行轻微增强，提高对比度
        const avgValue = value.sum / value.count;
        result[index++] = [xIndex, yIndex, avgValue];
      }

      return result;
    },
    // 添加采样方法
    sampleHeatmapData(data, sampleRatio = 0.1) {
      if (data.length <= 100000) return data;

      const sampled = [];
      const step = Math.max(1, Math.floor(1 / sampleRatio));

      // 系统采样，避免随机性带来的视觉偏差
      for (let i = 0; i < data.length; i += step) {
        sampled.push(data[i]);
      }

      return sampled;
    },
    renderHeatmapFor500k () {
      if (!this.heatmapData || !this.metadata) return;

      let displayData;
      const dataLength = this.heatmapData.data.length;

      if (dataLength > 200000) {
        // 超大数据集：先采样再聚合
        const sampledData = this.sampleHeatmapData(this.heatmapData.data, 0.15); // 5%采样
        displayData = this.aggregateHeatmapData(sampledData);
      } else if (dataLength > 100000) {
        displayData = this.aggregateHeatmapData(this.heatmapData.data);
      } else {
        displayData = this.heatmapData.data;
      }

      const option = {
        title: {
          text: this.metadata.title,
          left: 'center',
          top:'50px',
          textStyle: {
            fontSize: 16,
            fontWeight: 'bold',
            color:"black"
          }
        },
        tooltip: {
          position: 'top',
          formatter: (params) => {
            const xIndex = params.value[0]
            const yIndex = params.value[1]
            const value = params.value[2]

            // 使用实际的坐标值
            const xValue = this.heatmapData.xAxis[xIndex].toFixed(1)
            const yValue = this.heatmapData.yAxis[yIndex].toFixed(1)

            return `
          <div style="text-align: left; padding: 8px;">
            <div><b>距离:</b> ${xValue} km</div>
            <div><b>高度:</b> ${yValue} m</div>
            <div><b>传播因子:</b> ${value} dB</div>
          </div>
        `
          },

          borderColor: '#777',
          borderWidth: 1,
          textStyle: {
            color: '#000',
            fontSize: 12
          }
        },
        grid: {
          left: '80px',
          right: '120px',
          bottom: '60px',
          top: '80px',
          containLabel: false
        },
        xAxis: {
          type: 'category',
          data: this.heatmapData.xAxis,
          name: this.metadata.x_label,
          nameLocation: 'middle',
          nameGap: 30,
          nameTextStyle: {
            fontSize: 12,
            fontWeight: 'bold'
          },
          axisLine: {
            lineStyle: {
              color: '#000000',
              width: 2
            }
          },
          axisTick: {
            alignWithLabel: true,
            color: '#000000'
          },
          axisLabel: {
            fontSize: 10,
            color: '#000000',
            formatter: (value, index) => {
              // 显示部分刻度标签
              if (index % Math.ceil(this.heatmapData.xAxis.length / 8) === 0) {
                return value
              }
              return ''
            }
          },
          splitLine: {
            show: true,
            lineStyle: {
              type: 'dashed',
              color: '#ffffff'
            }
          }
        },
        yAxis: {
          type: 'category',
          data: this.heatmapData.yAxis,
          name: this.metadata.y_label,
          nameLocation: 'middle',
          nameGap: 5,
          nameTextStyle: {
            fontSize: 12,
            fontWeight: 'bold'
          },
          axisLine: {
            lineStyle: {
              color: '#000000',
              width: 2
            }
          },
          axisTick: {
            alignWithLabel: true,
            color:'#000000'
          },
          axisLabel: {
            fontSize: 10,
            color:'#000000',
            formatter: (value, index) => {
              // 显示部分刻度标签
              if (index % Math.ceil(this.heatmapData.yAxis.length / 32) === 0) {
                const numValue = Number(value)
                return isNaN(numValue) ? String(value) : numValue.toFixed(2)
              }
              return ''
            }
          },
          splitLine: {
            show: true,
            lineStyle: {
              type: 'dashed',
              color: '#ffffff'
            }
          }
        },
        visualMap: {
          type: 'continuous',
          min: this.metadata.value_range[0],
          max: this.metadata.value_range[1],
          calculable: true,
          orient: 'vertical',
          right: '40px',
          top: 'center',
          textStyle: {
            color: '#000',
            fontSize: 10
          },
          inRange: {
            color: [
              '#313695', '#4575b4', '#74add1', '#abd9e9',
              '#e0f3f8', '#ffffbf', '#fee090', '#fdae61',
              '#f46d43', '#d73027', '#a50026'
            ]
          },
          formatter: (value) => {
            const numValue = Number(value)
            return isNaN(numValue) ? value + ' dB' : numValue.toFixed(2) + ' dB'
          }
        },
        series: [{
          name: '传播因子',
          type: 'heatmap',
          data: displayData,
          large: true,
          progressive: 500,
          progressiveThreshold: 10000,
          hoverAnimation: false,
          legendHoverLink: false,
          selectedMode: false,
          itemStyle: {
            borderWidth: 0,
            borderColor: '#000000',
            gapWidth: 0,
          },
          // 关键调整：优化热力图显示参数
          pointSize: 5,           // 增大点尺寸
          blurSize: 4,            // 减小模糊半径，让颜色更集中
          minOpacity: 0.9,        // 大幅提高最小透明度
          maxOpacity: 1.0,        // 最大透明度设为1
          label: {
            show: false
          },
          emphasis: {
            itemStyle: {
              borderColor: '#000',
              borderWidth: 2,
              shadowBlur: 10,
              shadowColor: 'rgba(0, 0, 0, 0.5)'
            }
          },
          renderMode: 'accurate',
          animation: false
        }]
      }

      this.chart.setOption(option, {
        notMerge: true,
        lazyUpdate: true,
        replaceMerge: ['series'] // 替换而不是合并系列
      });


      // 添加鼠标移动事件监听
      this.chart.on('mousemove', (params) => {
        if (params.componentType === 'series' && params.seriesType === 'heatmap') {
          // 当鼠标在热力图数据点上移动时
          const xIndex = params.value[0];
          const yIndex = params.value[1];
          const value = params.value[2];

          const xValue = this.heatmapData.xAxis[xIndex];
          const yValue = this.heatmapData.yAxis[yIndex];

          // 将数据赋值给变量
          this.currentHoverData = {
            x: xValue,
            y: yValue,
            value: value,
            xIndex: xIndex,
            yIndex: yIndex
          };

          // 在控制台输出数据
          console.log('热力图鼠标位置数据:', {
            '距离 (km)': xValue.toFixed(1),
            '高度 (m)': yValue.toFixed(1),
            '传播因子 (dB)': value,
            'X轴索引': xIndex,
            'Y轴索引': yIndex
          });
          this.CPRange = xValue.toFixed(1);
          this.CPAltitude = yValue.toFixed(1);
          this.CPvalue = value.toFixed(1);



        } else {
          // 鼠标在空白位置时清空数据
          this.currentHoverData = null;
          console.log('鼠标在热力图空白位置');
        }
      });

      // 添加鼠标移出图表区域的事件
      this.chart.on('mouseout', (params) => {
        this.currentHoverData = null;
        console.log('鼠标移出热力图区域');
      });


      // 添加窗口调整大小监听
      window.addEventListener('resize', () => {
        this.chart.resize()
      })
    },


    showBigInfo(src) {
      this.showBig = true;
      this.bigUrl = src;
    },
    DQ6info(index) {
      var aaa = this.list[index]
      this.form6.M_units.push(aaa[0]);
      this.form6.altitude.push(aaa[1]);
    },
    propagation() {
      if (this.src2 != ""){
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          method: "get",//get请求方式
          params: { urls: this.lasted },
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'GET',
            'Access-Control-Request-Headers': 'content-type',
          }, 
        }).then((res) => {
          this.src2 = res.data.results[0].url
        })
      }
    },
    pathLoss() {
      console.log("1111111")
      this.$axios({
        url: "http://127.0.0.1:9084/pathLoss",
        method: "post",
        headers: {
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((response) => {
        console.log(response);
        if (response.data.success) {
          this.heatmapData = response.data.heatmap_data
          this.metadata = response.data.metadata

          // this.initChart();

          this.chart.resize();
          this.renderHeatmapFor500k();
          this.showJZ = false;




        } else {
          this.error = response.data.error || '数据加载失败'
        }
      })  
    },
    //计算相关的
    LDWLT() {
      var dataFinal = {
        "max_range": this.maxRange,
        "max_altitude": this.maxAltitude,
        "range_step": this.range_step,
        "altitude_step": this.altitude_step,
        "analysis_type": this.analysis_type,
        "polarization": this.polarization,
        "Horizontal": this.Horizontal,
        "beamwidth": this.beamwidth,
        "elevation_angle": this.elevation_angle,
        "antenna_height": this.antenna_height,
        "frequency": this.frequency,
        "surface_type": this.surface_type,
        "surface_type_combobox": this.surface_type_combobox,
        "dielectric_constant": this.dielectric_constant,
        "conductivity": this.conductivity,
        "refractivity_type": this.refractivity_type,
        "refractivity_type_combobox": this.refractivity_type_combobox,
        "Range": this.Range,
        "Profile": this.Profile,
        "terrain_type": this.terrain_type,
        "interpolation_type": this.interpolation_type,
        "num_points": this.num_points,
        "tRange": this.tRange,
        "Height": this.Height,
        // "plotType": this.plotType,
      }
      this.showJZ = true;
      console.log(dataFinal)
      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9084/LDWLT",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((response) => {

        console.log(response);


        if (response.data.success) {
          this.heatmapData = response.data.heatmap_data
          this.metadata = response.data.metadata

          this.initChart();

          this.chart.resize();
          this.renderHeatmapFor500k();
          this.showJZ = false;




        } else {
          this.error = response.data.error || '数据加载失败'
        }



        // var img = res.data[0];
        // this.lasted = res.data[0];
        // this.colorbarMin = res.data[1]
        // this.colorbarMax = res.data[2]
        // this.$axios({
        //   // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        //   url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
        //   method: "get",//get请求方式
        //   params: { urls: img },
        //   headers: {
        //     'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
        //     'Access-Control-Request-Method': 'GET',
        //     'Access-Control-Request-Headers': 'content-type',
        //   },
        // }).then((res) => {
        //   console.log(res)
        //   this.src2 = res.data.results[0].url
        // }).finally(() => {
        //   this.showJZ = false;
        //   console.log(this.showJZ)
        // })
      })
    },
    async DXT() {
      var dataFinal = {
        "max_range": this.maxRange,
        "max_altitude": this.maxAltitude,
        "range_step": this.range_step,
        "altitude_step": this.altitude_step,
        "analysis_type": this.analysis_type,
        "polarization": this.polarization,
        "Horizontal": this.Horizontal,
        "beamwidth": this.beamwidth,
        "elevation_angle": this.elevation_angle,
        "antenna_height": this.antenna_height,
        "frequency": this.frequency,
        "surface_type": this.surface_type,
        "surface_type_combobox": this.surface_type_combobox,
        "dielectric_constant": this.dielectric_constant,
        "conductivity": this.conductivity,
        "refractivity_type": this.refractivity_type,
        "refractivity_type_combobox": this.refractivity_type_combobox,
        "Range": this.Range,
        "Profile": this.Profile,
        "terrain_type": this.terrain_type,
        "interpolation_type": this.interpolation_type,
        "num_points": this.num_points,
        "tRange": this.tRange,
        "Height": this.Height,
      }
      const res = await this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9084/DXT",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {
          'Origin': 'http://127.0.0.1:8080',
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      });
      return res
    },


    //大气波导
    DQ1() {
      var dataFinal = {
        "M_entry": this.form1.M_entry,
        "altitude_entry": this.form1.altitude_entry,
        "max_altitude": this.maxAltitude,

      }
      console.log(dataFinal)
      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9084/LDWLTbd1",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res);
        var img1 = res.data;
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          method: "get",//get请求方式
          params: { urls: img1 },
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'GET',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)
          this.src3 = res.data.results[0].url
        })
      })

    },
    DQ2() {
      console.log(this.max_altitude)
      var dataFinal = {
        "S_M_entry": this.form2.S_M_entry,
        "s_altitude_entry": this.form2.s_altitude_entry,
        "S_M_entry1": this.form2.S_M_entry1,
        "s_altitude_entry1": this.form2.s_altitude_entry1,
        "S_M_entry2": this.form2.S_M_entry2,
        "s_altitude_entry2": this.form2.s_altitude_entry2,
        "max_altitude": this.maxAltitude,

      }

      console.log(dataFinal)
      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9084/LDWLTbd2",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {

          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res);
        var img1 = res.data;
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          method: "get",//get请求方式
          params: { urls: img1 },
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'GET',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)
          this.src4 = res.data.results[0].url
        })
      })

    },
    DQ3() {
      console.log(this.max_altitude)
      var dataFinal = {
        "S_b_M_entry": this.form3.S_M_entry,
        "s_b_altitude_entry": this.form3.s_altitude_entry,
        "S_b_M_entry1": this.form3.S_M_entry1,
        "s_b_altitude_entry1": this.form3.s_altitude_entry1,
        "S_b_M_entry2": this.form3.S_M_entry2,
        "s_b_altitude_entry2": this.form3.s_altitude_entry2,
        "S_b_M_entry3": this.form3.S_M_entry3,
        "s_b_altitude_entry3": this.form3.s_altitude_entry3,
        "max_altitude": this.maxAltitude,

      }

      console.log(dataFinal)
      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9084/LDWLTbd3",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {

          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res);
        var img1 = res.data;
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          method: "get",//get请求方式
          params: { urls: img1 },
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'GET',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)
          this.src5 = res.data.results[0].url
        })
      })

    },
    DQ4() {
      console.log(this.max_altitude)
      var dataFinal = {

        "e_M_entry": this.form4.e_M_entry,
        "e_altitude_entry": this.form4.e_altitude_entry,
        "e_M_entry1": this.form4.e_M_entry1,
        "e_altitude_entry1": this.form4.e_altitude_entry1,
        "e_M_entry2": this.form4.e_M_entry2,
        "e_altitude_entry2": this.form4.e_altitude_entry2,
        "e_M_entry3": this.form4.e_M_entry3,
        "e_altitude_entry3": this.form4.e_altitude_entry3,
        "max_altitude": this.maxAltitude,

      }

      console.log(dataFinal)
      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9084/LDWLTbd4",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {

          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res);
        var img1 = res.data;
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          method: "get",//get请求方式
          params: { urls: img1 },
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'GET',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)
          this.src6 = res.data.results[0].url
        })
      })

    },
    DQ5() {
      var dataFinal = {
        "typeRight": this.form5.typeRight,
        "typeLeft": this.form5.typeLeft,
        "max_altitude": this.form5.max_altitude,
        "atmosferikSicaklik": this.form5.atmosferikSicaklik,
        "denizYuzeySicakligi": this.form5.denizYuzeySicakligi,
        "atmosferikBasinc": this.form5.atmosferikBasinc,
        "bagilNem": this.form5.bagilNem,
        "spesifikNem": this.form5.spesifikNem,
        "baslangicPotansiyelSicakligi": this.form5.baslangicPotansiyelSicakligi,
        "ruzgarHizi": this.form5.ruzgarHizi,
        "ruzgarHiziOlcumYuksekligi": this.form5.ruzgarHiziOlcumYuksekligi,
        "havaSicakligiOlcumYuksekligi": this.form5.havaSicakligiOlcumYuksekligi,
        "bagilNemOlcumYuksekligi": this.form5.bagilNemOlcumYuksekligi,
        "ortalamaYuzeyKatmanSicakligi": this.form5.ortalamaYuzeyKatmanSicakligi,
        "suBuhariBasinci": this.form5.suBuhariBasinci,
      }

      console.log(dataFinal)
      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9084/LDWLTbd5",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {

          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res);
        var img1 = res.data;
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          method: "get",//get请求方式
          params: { urls: img1 },
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'GET',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)
          this.src7 = res.data.results[0].url
        })
      })

    },
    DQ6() {
      console.log(this.max_altitude)
      var dataFinal = {
        "newList": [],
      }
      for (let index = 0; index < this.form6.M_units.length; index++) {
        dataFinal.newList.push([this.form6.M_units[index], this.form6.altitude[index]]);
      }
      console.log(dataFinal)
      this.$axios({
        // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
        url: "http://127.0.0.1:9084/LDWLTbd6",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal,
        headers: {

          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res);
        var img1 = res.data;
        this.$axios({
          // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          method: "get",//get请求方式
          params: { urls: img1 },
          headers: {
            'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
            'Access-Control-Request-Method': 'GET',
            'Access-Control-Request-Headers': 'content-type',
          },
        }).then((res) => {
          console.log(res)
          this.src8 = res.data.results[0].url
        })
      })

    },
    save() {
      var dataFinal = {
        "max_range": this.maxRange,
        "max_altitude": this.maxAltitude,
        "range_step": this.range_step,
        "altitude_step": this.altitude_step,
        "analysis_type": this.analysis_type,
        "polarization": this.polarization,
        "Horizontal": this.Horizontal,
        "beamwidth": this.beamwidth,
        "elevation_angle": this.elevation_angle,
        "antenna_height": this.antenna_height,
        "frequency": this.frequency,
        "surface_type": this.surface_type,
        "surface_type_combobox": this.surface_type_combobox,
        "dielectric_constant": this.dielectric_constant,
        "conductivity": this.conductivity,
        "refractivity_type": this.refractivity_type,
        "refractivity_type_combobox": this.refractivity_type_combobox,
        "Range": this.Range,
        "Profile": this.Profile,
        "terrain_type": this.terrain_type,
        "interpolation_type": this.interpolation_type,
        "num_points": this.num_points,
        "tRange": this.tRange,
        "Height": this.Height,
      }
      this.dataFinal1.jsId = this.$route.query.id;
      this.dataFinal1.jsResult = JSON.stringify(dataFinal);
      this.dataFinal1.allImg = this.src1 + "," + this.src2;
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
    save1() {
      this.dataFinal1.jsId = this.$route.query.id;
      this.dataFinal1.jsResult = JSON.stringify(this.form1);
      this.dataFinal1.allImg = this.src3;
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
    save2() {
      this.dataFinal1.jsId = this.$route.query.id;
      this.dataFinal1.jsResult = JSON.stringify(this.form2);
      this.dataFinal1.allImg = this.src4;
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
    save3() {
      this.dataFinal1.jsId = this.$route.query.id;
      this.dataFinal1.jsResult = JSON.stringify(this.form3);
      this.dataFinal1.allImg = this.src5;
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
    save4() {
      this.dataFinal1.jsId = this.$route.query.id;
      this.dataFinal1.jsResult = JSON.stringify(this.form4);
      this.dataFinal1.allImg = this.src6;
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
    save5() {
      this.dataFinal1.jsId = this.$route.query.id;
      this.dataFinal1.jsResult = JSON.stringify(this.form5);
      this.dataFinal1.allImg = this.src7;
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
    save6() {
      this.dataFinal1.jsId = this.$route.query.id;
      this.dataFinal1.jsResult = JSON.stringify(this.form6);
      this.dataFinal1.allImg = this.src8;
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

    getLabel(value, list) {
      const item = list.find(item => item.value === value.toString());
      return item ? item.label : '';
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
    showOptions() {
      this.showOption = !this.showOption;
      this.atmosphereOption = false;
      this.atmosphereOptionP = false;
      this.surfaceOption = false;
      this.terrainOption = false;
      this.typePic1 = !this.typePic1;
      this.typePic2 = false;
      this.typePic3 = false;
      this.typePic4 = false;
    },
    showAtmosphereOption() {
      this.atmosphereOption = !this.atmosphereOption;
      this.showOption = false;
      this.atmosphereOptionP = false;
      this.surfaceOption = false;
      this.terrainOption = false;
      this.typePic2 = !this.typePic2;
      this.typePic1 = false;
      this.typePic3 = false;
      this.typePic4 = false;
      this.typePic5 = false;
    },
    showAtmosphereOptionP() {
      this.atmosphereOptionP = !this.atmosphereOptionP;
      this.showOption = false;
      this.atmosphereOption = false;
      this.surfaceOption = false;
      this.terrainOption = false;
      this.typePic3 = !this.typePic3;
      this.typePic1 = false;
      this.typePic2 = false;
      this.typePic4 = false;
      this.typePic5 = false;
    },
    showSurfaceOption() {
      this.surfaceOption = !this.surfaceOption;
      this.showOption = false;
      this.atmosphereOption = false;
      this.atmosphereOptionP = false;
      this.terrainOption = false;
      this.typePic4 = !this.typePic4;
      this.typePic1 = false;
      this.typePic2 = false;
      this.typePic3 = false;
      this.typePic5 = false;
    },
    showTerrainOption() {
      this.terrainOption = !this.terrainOption;
      this.showOption = false;
      this.atmosphereOption = false;
      this.atmosphereOptionP = false;
      this.surfaceOption = false;
      this.typePic5 = !this.typePic5;
      this.typePic1 = false;
      this.typePic2 = false;
      this.typePic3 = false;
      this.typePic4 = false;
    },
    selectOption(option) {
      this.polarization = option.value;
      this.showOption = false;
      this.typePic1 = false;
    },
    selectAtmosphereOption(option) {
      console.log(option.value)
      this.refractivity_type_combobox = option.value;
      this.atmosphereOption = false;
      this.typePic2 = false;


      if (this.refractivity_type_combobox == "Standard atmosphere") {
        this.dialogSAPVisible = true
      }

      if (this.refractivity_type_combobox == "Surface duct") {
        this.dialogSDVisible = true
      }
      if (this.refractivity_type_combobox == "Surface-based") {
        this.dialogSBDVisible = true
      }
      if (this.refractivity_type_combobox == "Elevated duct") {
        this.dialogEDVisible = true
      }
      if (this.refractivity_type_combobox == "Evaporation duct") {
        this.dialogEvaDVisible = true
      }
      if (this.refractivity_type_combobox == "User defined") {
        this.dialogUDVisible = true
      }


    },



    selectAtmosphereOptionP(option) {
      this.Profile = option.value;
      this.atmosphereOptionP = false;
      this.typePic3 = false;
    },
    selectSurfaceOption(option) {
      this.surface_type_combobox = option.value;
      this.surfaceOption = false;
      this.typePic4 = false;
    },
    selectTerrainOption(option) {
      this.interpolation_type = option.value;
      this.terrainOption = false;
      this.typePic5 = false;
    },
  },
  mounted() {
    this.initChartDown()
  },
  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose()
    }
  },

};
</script>

<style scoped>
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

.button {
  width: auto;
  min-width: 3.5vw;
  height: 1.2vw;
  padding: 0 0.3vw;
  background-color: #3967a4;
  text-align: center;
  font-size: 0.9vw;
  color: white;
  box-shadow: 0px 0px 10px #69cbff inset;
  line-height: 1.2vw;
  align-items: center;
}

.scrollable-content {
  width: 100%;
  height: 100%;
  overflow: auto;
  scrollbar-width: none;
  /* Firefox */
}

/deep/ .allInf01 .el-checkbox__inner {
  width: 0.8vw;
  height: 0.8vw;
}


/deep/ .allInf01 .el-checkbox__inner::after {
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

  /* overflow-y: auto; */
  /* 添加垂直滚动条 */
}

.doubleForm .el-form-item {
  width: 8vw;
}

.doubleForm .el-form-item__label {
  text-align: center;
}

/deep/ .allInf01 .el-form-item__label {
  color: #fff;
  width: 4vw;
  text-align: left;
  font-size: 0.7vw;
  line-height: 4vh;
  height: 100%;
}

/deep/ .allInf01 .el-form-item input-with-unit {
  height: 0.5vw;
}

/deep/.allInf01 .el-input__inner {
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

/deep/.allInf01 .el-input {
  width: 6vw;
  height: 100%;
  font-size: 0;
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  /* width: 80%; */
}

/deep/.allInf01 .el-radio {
  color: #f0f0f0;
  padding: 0;
  margin: 0;
  width: 6.8vw;
  align-items: center;
  /* 新增对齐样式 */
  display: inline-flex;
  vertical-align: middle;
  line-height: normal;
}

/deep/.allInf01 .el-radio__input {
  display: flex;
  align-items: center;
}

/deep/ .allInf01 .el-radio__label {
  padding-left: 0.6vw;
  font-size: 0.7vw;
  /* 新增对齐样式 */
  line-height: 1;
  display: flex;
  align-items: center;
}

::v-deep .el-radio.is-checked .el-radio__label {
  color: yellow;
}

/deep/ .allInf01 .el-radio__inner {
  border: 1px solid #DCDFE6;
  border-radius: 100%;
  width: 0.9vw;
  height: 0.9vw;
  cursor: pointer;
  box-sizing: border-box;
  display: flex;
  align-items: center;
}

.atmosphere-table {
  padding-bottom: 0.8vh;
}

.atmosphere-table table {
  padding-bottom: 0.5vh;
  width: 100%;
  border-top: 1px solid #0e6fdd;
  border-collapse: collapse;
}

.atmosphere-table tr {
  width: 100%;
}

.atmosphere-table th,
.atmosphere-table td {
  color: #fff;
  font-size: 0.9vw;
  /* min-width: 6vw; */
  /* padding: 0 0.5vw; */
  text-align: center;
  vertical-align: middle;
  height: 3vh;
  /* 匹配输入框高度 */
  align-items: center;
}

.atmosphere-table th:nth-child(1),
.atmosphere-table td:nth-child(1) {
  padding-left: 1vw;
  width: 7vw;
  /* 第一列宽度 */
}


.atmosphere-table th:nth-child(2),
.atmosphere-table td:nth-child(2) {
  /* padding-left: 1vw; */
}

.terrain-table {
  padding-bottom: 0.8vh;
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
  font-size: 0.9vw;
  width: 54%;
  padding: 0 0.5vw;
  text-align: center;
  vertical-align: middle;
  height: 3vh;
  /* 匹配输入框高度 */
  align-items: center;
}

.el-button /deep/ .el-button__inner {
  text-align: center;
  font-size: 0.7vw;
  border-radius: 0;
  color: #fff;
  border: none;
  background-color: transparent;
}

/deep/ .allInf01 .el-form-item__content {
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
  position: static;
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

.biaotouC {
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

.biaotou-left {
  width: 60%;
  display: flex;
  align-items: center;
  color: #fff;
  font-size: 1vw;
  white-space: nowrap;
  padding-left: 1vw;
  background-image: url('@/assets/img/qianbiao.png');
  background-repeat: no-repeat;
  background-position: left center;
  background-size: 0.6vw 0.4vh;
}

.biaotou-right {
  display: flex;
  align-items: center;
  color: #fff;
  font-size: 0.8vw;
  white-space: nowrap;
  padding-left: 1vw;
  background-image: url('@/assets/img/shuaxin.png');
  background-repeat: no-repeat;
  background-position: left center;
  background-size: 0.7vw auto;
}

.back4 img {
  border-radius: 1vw;
  height: 90%;
  object-fit: contain;

}

.back {
  display: flex;
  flex-direction: column;
  height: auto;
  margin-bottom: 1vh;
  border-radius: 10px;
  background-color: #006cda;
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
}

.backC {
  width: 33%;
  display: flex;
  flex-direction: column;
  height: 95%;
  margin-right: 0.2vw;
  border-radius: 10px;
  margin-bottom: 1vh;
  background-color: #006cda;
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

.picture-container {
  border-radius: 2vw;
  background-color:#006cda;
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  width: 100%;
  height: 27.5vh;

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
  width: 4vw;
  height: 2vh;
  margin-left: 1vw;
  align-items: center;
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
  width: 3vw;
  list-style: none;
  text-align: center;
  padding: 0.3vw;
  position: absolute;
  right: 1.5vw;
  top: 1.2vh;
  color: #fff;
  border-radius: 0.2vw;
  font-size: 0.8vw;
  z-index: 9999999;
  background-image: url('@/assets/img/optionBack.png');
  //background-repeat: no-repeat;
  background-size: cover;
}

.formactionC {
  height: 2.5vh;
  margin-bottom: 0.5vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: auto;
  /* margin: 0 0 0.3vh; */
  padding: 0 0.5vw;
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  line-height: 3vh;
  position: relative;
  overflow: visible;
  justify-items: center;
}

.formactionC /deep/.el-input {
  width: auto;
  display: flex;
  align-items: center;
  height: 100%;
}

.formactionC /deep/.el-input__inner {
  width: 4vw;
  display: flex;
  align-items: center;
  height: 100%;
}

.formaction {
  margin-bottom: 0.5vh;
  height: 2.5vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 85%;
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  line-height: 3vh;
  position: relative;
  overflow: visible;
  padding-left: 2.5vw;
  justify-items: center;
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

.onfocus-style {
  background-image: url('@/assets/img/xuanzhongduan.png');
  background-size: 108% auto;
  background-position: center;
  background-repeat: no-repeat;
}

.formaction1 {
  height: 2.5vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: auto;
  padding: 0 1.5vw 0 2.2vw;
  color: #fff;
  font-size: 0.9vw;
  white-space: nowrap;
  line-height: 3vh;
  position: relative;
}

.formaction1 .el-input {
  width: 4vw;
  display: flex;
  align-items: center;
  height: 100%;
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
  margin-left: 1vw;
  background-color:#196EC1;
  color: #FFFFFF;
  font-weight: bold;
}

.buttonRun {
  height: 2vw;
  width: 33%;
  border-radius: 2vw;
  line-height: 0.1vw;
  background-color:#196EC1;
  background-repeat: no-repeat;
  background-size: 100% 100%;
  /* position: absolute;
  bottom: 1.3vw; */
  margin-top: -4vh;
  margin-left: 26vw;
  text-align: center;
  color: #FFFFFF;
  font-size: 1vw;

}

.image2 /deep/ .el-image__inner {
  height: 60%;
  width: auto;
  height: 100%;
  font-size: 0;
  display: flex;
  align-items: center;
}

.waibiankuang {
  border-top: 1px solid #196EC1;
  padding-top: 1vh;
  padding-left: 1vw;
}

.inputTz /deep/.el-input__inner {
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

.inputbg {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}
.selectInfo1 {
  width: 6.5vw;
  text-align: left;
  color: #fff
}
/deep/.showInfo1 .el-dialog{
  background-color: #FFFFFF;

}
/deep/.showInfo1 .el-dialog__title{
  color: #Ffffff;
}
/deep/.showInfo1 .el-form-item__label{
  color: #Ffffff;
}
.my-dialog {
  margin-top: 0px;
}
</style>
