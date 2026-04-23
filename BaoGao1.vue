<template>
  <div style="width: 100%;height: 100%;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:-1;" src="../assets/img/twbg.png">
    <headInfo></headInfo>

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
                <div class="oneMuluXuan" v-if="item.name === '辅助决策'">
                  <img src="../assets/img/twCircle.png"
                    style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 7%;">
                  <div style="width: 55%;text-align: center;">
                    {{ item.name }}
                  </div>
                  <img src="../assets/img/jiantouchoose.png"
                    style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 7%;">
                  <img src="../assets/img/muluchoose.png"
                    style="width: 19vw;height: 6vw;position: absolute;bottom: -3vw;left: -3.5vw;z-index: -1;" />
                </div>
                <div class="oneMulu" v-else @click="goInfo(item.info)">
                  <div style="width: 80%;text-align: center;">{{ item.name }}</div>
                  <img src="../assets/img/jiantou.png"
                    style="width: 0.9vw;height:0.9vw;object-fit: contain;float: right;margin-top: 13%;">
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="rightContent">
        <div
          style="background-color: rgba(255,255,255,0.51);width: 98.7%;height: 95.5%;position: absolute;z-index: -1;left: 1.2%;top: 4.5%;border-radius: 1vw;">
        </div>
        <!-- 侧边栏开启按钮 -->
        <div class="sidebar-toggle" @click="toggleSidebar" v-if="!sidebarVisible">
          <img src="../assets/img/jmtz.png" alt="打开侧边栏" />
        </div>
        <!--        v-if="showList"-->
        <!-- 侧边栏 -->
        <div class="showList" v-if="showList">
          <div
            style="color: #FFFFFF;height: 1vw;width: 98%;display: flex;align-items: center;margin-left: 2%;margin-bottom: 1vw;">
            <img src="../assets/img/baogaojian.png"
              style="height: 70%;object-fit: contain;justify-items: center;margin-right: 1%;">
            <div style="justify-items: center;">规则</div>
            <el-button type="primary" @click="addGz"
              style="margin-left: 1vw;width:3vw;height:2vh;display: flex;align-items: center;justify-content: center;margin-right: 1vw;">新增规则</el-button>
            <!-- <div style="width:3vw;margin-right: 1vw;height: 2vh;"> -->
            <el-button
              style="height: 100%;width: 3vw;text-align: center;display:flex;justify-content: center;align-items: center;margin-right: 1vw;margin-left: 0;"
              type="primary" @click="openFileInputData">导入规则</el-button>
            <input ref="fileInputData" type="file" accept=".sql" style="display: none;"
              @change="handleFileChangeData" />
            <!-- </div> -->
            <el-button
              style="height: 100%;width: 3vw;text-align: center;display:flex;justify-content: center;align-items: center;"
              type="primary" @click="exportSql">导出规则</el-button>
          </div>

          <!-- <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.2vw;" v-if="showYun">云</div> -->
          <!-- <el-table style="line-height: 0.5vw;width: 100%;" :data="yunlist" v-if="showYun">
            <el-table-column prop="text" label="规则内容" header-align="center" align="center">
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
</el-table-column>
</el-table> -->

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showYun">(一)云</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="yunlist" v-if="showYun">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则</el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showNJD">(二)能见度</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="njdlist" v-if="showNJD">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showQW">(一)气温</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="qwlist" v-if="showQW">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showFJJB">(二)飞机积冰</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="fjjblist" v-if="showFJJB">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showFeng">(三)风</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="fenglist" v-if="showFeng">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showJCYD">(四)舰船摇荡</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="jcydlist" v-if="showJCYD">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showJYY">(四)积雨云</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="jyylist" v-if="showJYY">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showCDB">超短波</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="cdblist" v-if="showCDB">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showDB">短波</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="dblist" v-if="showDB">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showTCJL">(一)雷达</div>
          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showTCJL">(1)探测距离</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="tcjllist" v-if="showTCJL">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showDQSJ">(2)大气衰减</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="dqsjlist" v-if="showDQSJ">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showHZB">(3)海杂波</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="hzblist" v-if="showHZB">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showSSPM">(二)声呐</div>
          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showSSPM">(1)声速剖面</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="sspmlist" v-if="showSSPM">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showHK">(2)海况</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="hklist" v-if="showHK">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showHL">(3)海流</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="hllist" v-if="showHL">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showNB">(4)内波</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="nblist" v-if="showNB">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showHYF">(5)海洋锋</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="hyflist" v-if="showHYF">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showZCDW">(6)中尺度涡</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="zcdwlist" v-if="showZCDW">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showKZXLD">(一)航空鱼雷</div>
          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showKZXLD">(1)空中下落段</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="kzxldlist" v-if="showKZXLD">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showXQXSD">(2)下潜寻深段</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="xqxsdlist" v-if="showXQXSD">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showSSD">(3)搜索段</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="ssdlist" v-if="showSSD">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showGZD">(4)跟踪段</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="gzdlist" v-if="showGZD">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 0.5vw;" v-if="showZSJTF">(二)空舰导弹</div>
          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showZSJTF">(1)直升机突防</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="zsjtflist" v-if="showZSJTF">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showDDDD">(2)导弹弹道</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="ddddlist" v-if="showDDDD">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div style="color: #FFFFFF;margin-bottom: 0.1vw;margin-left: 1.5vw;" v-if="showDDMZD">(3)导弹末制导</div>
          <el-table style="line-height: 0.5vw;width: 100%;" :data="ddmzdlist" v-if="showDDMZD">
            <el-table-column label="规则内容" header-align="center" align="center">
              <template slot-scope="scope">
                <div v-html="scope.row.text"></div>
              </template>
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="useGz(scope.row)">使用规则
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <div
            style="color: #FFFFFF;height: 1vw;width: 98%;display: flex;align-items: center;margin-left: 2%;margin-bottom: 1vw;">
            <img src="../assets/img/baogaojian.png"
              style="height: 70%;object-fit: contain;justify-items: center;margin-right: 1%;">
            <div style="justify-items: center;">计算</div>
          </div>
          <el-table style="line-height: 0.5vw;" :data="qjjslist" v-if="isQjjs">
            <el-table-column prop="name" label="计算名称" header-align="center" align="center">
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="historyJs(scope.row)">计算记录
                </el-button>
                <el-button size="mini" type="warning" @click="useJs(scope.row)">新增计算
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <el-table style="line-height: 0.5vw;" :data="fxjslist" v-if="isFxjs">
            <el-table-column prop="name" label="计算名称" header-align="center" align="center">
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="historyJs(scope.row)">计算记录
                </el-button>
                <el-button size="mini" type="warning" @click="useJs(scope.row)">新增计算
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <el-table style="line-height: 0.5vw;" :data="tcjslist" v-if="isTcjs">
            <el-table-column prop="name" label="计算名称" header-align="center" align="center">
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="historyJs(scope.row)">计算记录
                </el-button>
                <el-button size="mini" type="warning" @click="useJs(scope.row)">新增计算
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <el-table style="line-height: 0.5vw;" :data="txjslist" v-if="isTxjs">
            <el-table-column prop="name" label="计算名称" header-align="center" align="center">
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="historyJs(scope.row)">计算记录
                </el-button>
                <el-button size="mini" type="warning" @click="useJs(scope.row)">新增计算
                </el-button>
              </template>
            </el-table-column>
          </el-table>

          <el-table style="line-height: 0.5vw;" :data="gjjslist" v-if="isGjjs">
            <el-table-column prop="name" label="计算名称" header-align="center" align="center">
            </el-table-column>
            <el-table-column prop="option" label="操作" header-align="center" align="center">
              <template slot-scope="scope">
                <el-button size="mini" type="warning" @click="historyJs(scope.row)">计算记录
                </el-button>
                <el-button size="mini" type="warning" @click="useJs(scope.row)">新增计算
                </el-button>
              </template>
            </el-table-column>
          </el-table>
        </div>
        <div class="sidebar" :class="{ 'sidebar-visible': sidebarVisible }">
          <div class="sidebar-header">
            <div class="sidebar-close" @click="toggleSidebar">
              <img src="../assets/img/jmtzyz.png" alt="关闭侧边栏" />
            </div>
          </div>
          <div class="sidebar-content">
            <div class="sidebar-item" v-for="(item, index) in sidebarItems" :key="index"
              @mouseenter="selectSidebarItem(index)" :class="{ 'sidebar-item-active': selectedSidebarItem === index }">
              {{ item }}
            </div>

          </div>
        </div>


        <div class="contentInfo" style="position: relative;margin-top: 4%;">


          <div
            style="width: 22vw;height: 2.2vw;margin-bottom: 1vw;margin-top: 2vh;position: absolute;right: -12vw;display: flex;z-index: 2000;">
            <el-button style="height: 100%;width: 5vw;text-align: center;display:flex;justify-content: center;"
              type="primary" @click="openDialog">历史检索</el-button>
            <!-- <el-button style="height: 100%;width: 5vw;text-align: center;display:flex;justify-content: center;"
              type="warning" @click="getAllTable">
              列表设置
            </el-button> -->
          </div>

          <div class="contentBox1">
            <div style="height: 1.8vw;margin-bottom: 1vw;margin-top: 2vh;position: relative;">
              <img src="../assets/img/baogaoDH.png"
                style="height: 100%;object-fit: contain;position: absolute;z-index: -1;">
              <div style="font-size: 1vw;margin-left: 4%;line-height: 1.8vw;">任务名称</div>
            </div>
            <div class="graphcontains1">
              <div class="custom-select" @click="toggleOptions1">
                <div style="font-size: 1vw;width: 10vw;">飞机任务:</div>
                <div style="width: 20vw;position: relative;">
                  <img src="../assets/img/graphInput.png"
                    style="position: absolute;z-index: -1;width:100%;height: 100%;background-color: rgba(0, 161, 255, 0.58);border-radius: 1vw;">

                  <div class="selected-option">
                    {{ this.rwmc.text }}
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
          </div>
          <div class="contentBox2" style="margin-top: 0.5vw;">
            <div style="height: 1.8vw;margin-bottom: 1vw;position: relative;">
              <img src="../assets/img/baogaoDH.png"
                style="height: 100%;object-fit: contain;position: absolute;z-index: -1;">
              <div style="font-size: 1vw;margin-left: 4%;line-height: 1.8vw;">任务目的</div>
            </div>
            <div style="width: 90%;height: 4vw;margin-left: 5%;">
              <el-input type="textarea" :rows="3" placeholder="请输入任务目的" v-model="rwmd">
              </el-input>
            </div>
          </div>
          <div class="contentBox3" style="margin-top: 0.5vw;">
            <div style="height: 1.8vw;margin-bottom: 1vw;position: relative;">
              <img src="../assets/img/baogaoDH.png"
                style="height: 100%;object-fit: contain;position: absolute;z-index: -1;">
              <div style="font-size: 1vw;margin-left: 4%;line-height: 1.8vw;">任务时间</div>
            </div>
            <div style="width: 90%;height: 4vw;margin-left: 5%;">
              <el-date-picker v-model="rwsj" type="datetime" @change="showTime" placeholder="选择日期时间"
                style="color: #fff;">
              </el-date-picker>
            </div>
          </div>
           <div class="contentBox6">
            <div style="height: 1.8vw;margin-bottom: 1vw;position: relative;">
              <img src="../assets/img/baogaoDH.png"
                style="height: 100%;object-fit: contain;position: absolute;z-index: -1;">
              <div style="font-size: 1vw;margin-left: 4%;line-height: 1.8vw;">任务海区</div>
            </div>
            <div style="width: 90%;height: 4vw;margin-left: 5%;">
              <el-input type="textarea" :rows="3" placeholder="请输入任务海区" v-model="rwhq">
              </el-input>
            </div>
          </div>
          <div class="contentBox5">
            <div style="height: 1.8vw;margin-bottom: 1vw;position: relative;">
              <img src="../assets/img/baogaoDH.png"
                style="height: 100%;object-fit: contain;position: absolute;z-index: -1;">
              <div style="font-size: 1vw;margin-left: 4%;line-height: 1.8vw;">任务兵力</div>
            </div>
            <div style="font-size: 0.9vw;margin-bottom: 1vw;">（一）舰艇</div>
            <div class="graphcontains2">
              <div class="custom-select" @click="toggleOptions2">
                <div style="font-size: 1vw;width: 10vw;">舰艇型号:</div>
                <div style="width: 20vw;position: relative;">
                  <img src="../assets/img/graphInput.png"
                    style="position: absolute;z-index: -1;width:100%;height: 100%;background-color: rgba(0, 161, 255, 0.58);border-radius: 1vw;">

                  <div class="selected-option">
                    {{ this.jtxh.text }}
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
            <div style="font-size: 0.9vw;margin-bottom: 1vw;">（二）舰载直升机</div>
            <div class="graphcontains2">
              <div class="custom-select" @click="toggleOptions3">
                <div style="font-size: 1vw;width: 10vw;"> 飞机型号:</div>
                <div style="width: 20vw;position: relative;">
                  <img src="../assets/img/graphInput.png"
                    style="position: absolute;z-index: -1;width:100%;height: 100%;background-color: rgba(0, 161, 255, 0.58);border-radius: 1vw;">

                  <div class="selected-option">
                    {{ this.fjxh.text }}
                  </div>
                  <img src="../assets/img/graphDown.png"
                    style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                    v-if="typePic3 == 0">
                  <img src="../assets/img/graphUp.png"
                    style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                    v-if="typePic3 == 1">
                  <ul v-if="showOptions3" class="options">
                    <li v-for="(option, index) in options3" :key="index" @click="selectOption3(option)" class="option">
                      {{ option.label }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
         
          <div class="contentBox4">
            <div style="height: 1.8vw;margin-bottom: 1vw;position: relative;">
              <img src="../assets/img/baogaoDH.png"
                style="height: 100%;object-fit: contain;position: absolute;z-index: -1;">
              <div style="font-size: 1vw;margin-left: 4%;line-height: 1.8vw;">任务环境</div>
            </div>
            <div style="width: 90%;margin-left: 5%;position: relative;" class="bg">
              <el-table :data="[rwhj[0].firstRow]" header-align="center" style="width: 100%" :key="indexNum">
                <el-table-column v-for="column in dynamicColumns" :key="column.prop" :prop="column.prop"
                  :label="column.label" :width="column.width" align="center">
                  <template slot-scope="scope">
                    <el-input v-model="scope.row[column.prop]" :placeholder="'请输入' + column.label"></el-input>
                  </template>
                </el-table-column>
              </el-table>
              <el-table :data="[rwhj[0].secondRow]" header-align="center" style="width: 100%" :key="indexNum">
                <el-table-column v-for="column in dynamicColumns1" :key="column.prop" :prop="column.prop"
                  :label="column.label" :width="column.width" align="center">
                  <template slot-scope="scope">
                    <el-input v-model="scope.row[column.prop]" :placeholder="'请输入' + column.label"></el-input>
                  </template>
                </el-table-column>
              </el-table>
            </div>
          </div>
          <div class="contentBox7" style="margin-top: 1vw;">
            <div style="height: 1.8vw;margin-bottom: 1vw;position: relative;">
              <img src="../assets/img/baogaoDH.png"
                style="height: 100%;object-fit: contain;position: absolute;z-index: -1;">
              <div style="font-size: 1vw;margin-left: 4%;line-height: 1.8vw;">环境分析</div>
            </div>
            <div style="font-size: 0.9vw;margin-bottom: 1vw;">（一）起降</div>
            <div
              style="width: 90%;height: 20vw;background-color: rgba(251,251,251,0.38);margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="showTp1">
              <div @click="loadPng" style="position: absolute;top: 0.5vw;z-index: 8000;right: 0.5vw;" class="icon2"
                title="导出图片">
                <i style="font-size: 2vw;" class="el-icon-picture"></i>
              </div>
              <div id="graph-panel" style="width: 100%;height: 100%;position: relative;"></div>
            </div>
            <div style="width: 90%;height: 20vw;margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="!showTp1 && qjtp !== ''">
              <img :src="qjtp" style="height: 100%;object-fit: contain;" />
            </div>
            <el-button type="primary" v-if="showTp1" style="margin-left: 5%;margin-bottom: 1vw;">导入计算结果
            </el-button>
            <div style="width: 90%;margin-left: 5%;" class="testInfo">
              <editor v-model="zzhjys" :config="editorConfig1" :disabled="true" />
            </div>
            <div style="width: 90%;margin-left: 5%;">
              <img :src="qjysImg" v-if="qjysImg != ''"
                style="width: 30%;height: 30%;object-fit: contain;margin-top: 1vw;" />
            </div>
            <div style="font-size: 0.9vw;margin-bottom: 1vw;margin-top: 1vw;">（二）飞行</div>
            <div
              style="width: 90%;height: 20vw;background-color: rgba(251,251,251,0.38);margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="showTp2">
              <div @click="loadPng1" style="position: absolute;top: 0.5vw;z-index: 8000;right: 0.5vw;" class="icon2"
                title="导出图片">
                <i style="font-size: 2vw;" class="el-icon-picture"></i>
              </div>
              <div id="graph-panel1" style="width: 100%;height: 100%;position: relative;">
              </div>
            </div>
            <div style="width: 90%;height: 20vw;margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="!showTp2 && fxtp !== ''">

              <img :src="fxtp" style="height: 100%;object-fit: contain;" />
            </div>
            <div style="width: 90%;margin-left: 5%;" class="testInfo">
              <editor v-model="fxhjys" :config="editorConfig2" placeholder="请输入飞行作战环境因素" :disabled="true" />
            </div>
            <div style="font-size: 0.9vw;margin-bottom: 1vw;margin-top: 1vw;">（三）通信载荷</div>
            <div
              style="width: 90%;height: 20vw;background-color: rgba(251,251,251,0.38);margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="showTp3">
              <div @click="loadPng2" style="position: absolute;top: 0.5vw;z-index: 8000;right: 0.5vw;" class="icon2"
                title="导出图片">
                <i style="font-size: 2vw;" class="el-icon-picture"></i>
              </div>
              <div id="graph-panel2" style="width: 100%;height: 100%;position: relative;">
              </div>
            </div>
            <div style="width: 90%;height: 20vw;margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="!showTp3 && txtp !== ''">

              <img :src="txtp" style="height: 100%;object-fit: contain;" />
            </div>
            <div class="graphcontains2">
              <div class="custom-select" @click="toggleOptions4">
                <div style="font-size: 1vw;width: 10vw;"> 通信载荷:</div>
                <div style="width: 20vw;position: relative;">
                  <img src="../assets/img/graphInput.png"
                    style="position: absolute;z-index: -1;width:100%;height: 100%;background-color: rgba(0, 161, 255, 0.58);border-radius: 1vw;">

                  <div class="selected-option">
                    {{ this.txzh.text }}
                  </div>
                  <img src="../assets/img/graphDown.png"
                    style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                    v-if="typePic4 == 0">
                  <img src="../assets/img/graphUp.png"
                    style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                    v-if="typePic4 == 1">
                  <ul v-if="showOptions4" class="options">
                    <li v-for="(option, index) in options4" :key="index" @click="selectOption4(option)" class="option">
                      {{ option.label }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <el-button type="primary" v-if="showTp3" style="margin-left: 5%;margin-bottom: 1vw;">导入计算结果
            </el-button>
            <div style="width: 90%;margin-left: 5%;" class="testInfo">
              <editor v-model="txzhys" :config="editorConfig3" placeholder="请输入环境对通信载荷的影响" :disabled="true" />
              <img :src="txzhysImg" v-if="txzhysImg != ''" style="width: 30%;object-fit: contain;margin-top: 1vw;" />
            </div>
            <div style="font-size: 0.9vw;margin-bottom: 1vw;margin-top: 1vw;">（四）探测载荷</div>
            <div
              style="width: 90%;height: 20vw;background-color: rgba(251,251,251,0.38);margin-left: 5%;margin-bottom: 1vw;position: relative"
              v-if="showTp4">
              <div @click="loadPng3" style="position: absolute;top: 0.5vw;z-index: 8000;right: 0.5vw;" class="icon2"
                title="导出图片">
                <i style="font-size: 2vw;" class="el-icon-picture"></i>
              </div>
              <div id="graph-panel3" style="width: 100%;height: 100%;position: relative;">
              </div>
            </div>
            <div style="width: 90%;height: 20vw;margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="!showTp4 && tctp !== ''">

              <img :src="tctp" style="height: 100%;object-fit: contain;" />
            </div>
            <div class="graphcontains2">
              <div class="custom-select" @click="toggleOptions5">
                <div style="font-size: 1vw;width: 10vw;"> 探测载荷:</div>
                <div style="width: 20vw;position: relative;">
                  <img src="../assets/img/graphInput.png"
                    style="position: absolute;z-index: -1;width:100%;height: 100%;background-color: rgba(0, 161, 255, 0.58);border-radius: 1vw;">

                  <div class="selected-option">
                    {{ tczh.text }}
                  </div>
                  <img src="../assets/img/graphDown.png"
                    style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                    v-if="typePic5 == 0">
                  <img src="../assets/img/graphUp.png"
                    style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                    v-if="typePic5 == 1">
                  <ul v-if="showOptions5" class="options">
                    <li v-for="(option, index) in options5" :key="index" @click="selectOption5(option)" class="option">
                      {{ option.label }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <el-button type="primary" @click="openJs(2)" v-if="showTp4">导入计算结果</el-button>
            <div style="width: 90%;margin-left: 5%;" class="testInfo">
              <editor v-model="tczhys" :config="editorConfig4" placeholder="请输入环境对探测载荷的影响" :disabled="true"
                :key="tczhysIndex" />
              <img :src="tczhysImg" v-if="tczhysImg != ''" style="width: 30%;object-fit: contain;margin-top: 1vw;" />
              <img :src="tczhysImg1" v-if="tczhysImg1 != ''" style="width: 30%;object-fit: contain;margin-top: 1vw;" />
            </div>
            <div style="font-size: 0.9vw;margin-bottom: 1vw;margin-top: 1vw;" v-if="showGJZH()">（五）攻击载荷</div>
            <div
              style="width: 90%;height: 20vw;background-color: rgba(251,251,251,0.38);margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="showTp5">
              <div @click="loadPng4" style="position: absolute;top: 0.5vw;z-index: 8000;right: 0.5vw;" class="icon2"
                title="导出图片">
                <i style="font-size: 2vw;" class="el-icon-picture"></i>
              </div>
              <div id="graph-panel4" style="width: 100%;height: 100%;position: relative;">
              </div>
            </div>
            <div style="width: 90%;height: 20vw;margin-left: 5%;margin-bottom: 1vw;position: relative;"
              v-if="!showTp5 && gjtp !== ''">

              <img :src="gjtp" style="height: 100%;object-fit: contain;" />
            </div>
            <div class="graphcontains2">
              <div class="custom-select" @click="toggleOptions6">
                <div style="font-size: 1vw;width: 10vw;"> 攻击载荷:</div>
                <div style="width: 20vw;position: relative;">
                  <img src="../assets/img/graphInput.png"
                    style="position: absolute;z-index: -1;width:100%;height: 100%;background-color: rgba(0, 161, 255, 0.58);border-radius: 1vw;">

                  <div class="selected-option">
                    {{ gjzh ? gjzh.text : '请选择攻击载荷' }}
                  </div>
                  <img src="../assets/img/graphDown.png"
                    style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                    v-if="typePic6 == 0">
                  <img src="../assets/img/graphUp.png"
                    style="position: absolute;z-index: 99;width: 5%;height: 100%;object-fit: contain;right: 0.5vw;top: 0;"
                    v-if="typePic6 == 1">
                  <ul v-if="showOptions6" class="options">
                    <li v-for="(option, index) in options6" :key="index" @click="selectOption6(option)" class="option">
                      {{ option.label }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <el-button type="primary" @click="openJs(3)" v-if="showTp5">导入计算结果</el-button>
            <div style="width: 90%;margin-left: 5%;" class="testInfo" v-if="showGJZH()">
              <editor v-model="gjzhys" :config="editorConfig5" placeholder="请输入环境对攻击载荷的影响" :disabled="true" />
              <img :src="gjzhysImg" v-if="gjzhysImg != ''" style="width: 30%;object-fit: contain;margin-top: 1vw;" />
            </div>
            <el-button style="width: 5vw;text-align: center;margin-top: 2vh;float: right;margin-right: 5vw;"
              type="primary" @click="baoCun">保存
            </el-button>
          </div>


        </div>
      </div>
    </div>

    <el-dialog title="表头信息管理" :visible.sync="showLieBiao">
      <el-button size="mini" type="success" @click="addLieBiao">新增
      </el-button>
      <el-table height="400" :data="lieBiaoList">
        <el-table-column prop="columName" label="表头名称" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="columkey" label="表头标识" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="option" label="操作" header-align="center" align="center">
          <template slot-scope="scope">
            <el-button size="mini" type="warning" @click="editLieBiao(scope.row)">修改表头
            </el-button>
          </template>
        </el-table-column>


      </el-table>
      <div slot="footer" class="dialog-footer">
        <el-button @click="showLieBiao = false">取 消</el-button>
        <el-button type="primary" @click="sumbitConlum">确 定</el-button>
      </div>
    </el-dialog>

    <el-dialog title="添加规则" :visible.sync="showGz" style="width: 60% !important;margin-left: 20%;" class="dialog1">
      <div style="border: 1px solid #ccc;margin-bottom: 2vh;">
        <Toolbar style="border-bottom: 1px solid #ccc" :editor="editor" :defaultConfig="toolbarConfig" :mode="mode" />
        <Editor style="height: auto; overflow-y: hidden;" v-model="gzwenben" :defaultConfig="editorConfig" :mode="mode"
          @onCreated="onCreated" />
      </div>
      <el-select v-model="gzType" placeholder="请选择规则分类" style="margin-bottom: 2vh;display: block;width: 11.5vw;"
        class="selectPlace">
        <el-option v-for="item in gzTypeList" :key="item.id" :label="item.label" :value="item.value" />
      </el-select>
      <el-select v-model="gzInfoType" placeholder="请选择一级分类" style="margin-bottom: 2vh;display: block;width: 11.5vw;"
        class="selectPlace">
        <el-option v-for="item in yjgzTypeList" :key="item.id" :label="item.label" :value="item.value" />
      </el-select>
      <el-select v-model="gzInfoType1" placeholder="请选择二级分类" style="margin-bottom: 2vh;display: block;width: 11.5vw;"
        class="selectPlace">
        <el-option v-for="item in ejgzTypeList" :key="item.id" :label="item.label" :value="item.value" />
      </el-select>
      <div>
        <el-button @click="showGz = false">取 消</el-button>
        <el-button type="primary" @click="submitGz">确 定</el-button>
      </div>
    </el-dialog>

    <el-dialog title="新增列信息" style="width: 100vw;height: 30vw;" :visible.sync="dialogTableVisible">
      <el-form :model="form">

        <el-form-item label="列名" :label-width="formLabelWidth">

          <el-select v-model="form.propName" placeholder="请选择列名" @change="handleChange">
            <el-option v-for="item in allTable" :key="item.columkey" :label="item.columName" :value="item.columName">
            </el-option>
          </el-select>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogTableVisible = false">取 消</el-button>
        <el-button type="primary" @click="sumbitConlum">确 定</el-button>
      </div>
    </el-dialog>


    <el-dialog title="报告名称" :visible.sync="dialogVisibleInput" width="30%">
      <div style="height: 100%;" class="divBg">
        <el-input v-model="baoGaoName" placeholder="请输入报告名称" style="margin-bottom: 1vw;width: 30%;margin-left: 1%;margin-top: 2%;"
        class="nameInput"></el-input>
      <div style="display: flex;">
        <el-button @click="dialogVisibleInput = false" style="width: 4vw;margin-left: 1%;">取 消</el-button>
        <el-button type="primary" @click="exportAllWord" style="width: 4vw;">确 定</el-button>
      </div>
      </div>

    </el-dialog>


    <el-dialog title="表头编辑" :visible.sync="showEdit" width="30%">
      <el-input v-model="comlunName" placeholder="请输入表头名称" style="margin-bottom: 1vw;"></el-input>
      <el-input v-model="comlunkey" placeholder="请输入表头标识" style="margin-bottom: 1vw;"></el-input>
      <el-button @click="showEdit = false">取 消</el-button>
      <el-button type="primary" @click="sumbitConlumInfo">确 定</el-button>

    </el-dialog>


    <el-dialog class="history" title="历史检索" :visible.sync="dialogVisibleList" width="50%" label-position="left">
      <el-select v-model="task" placeholder="请选择任务" class="head" style="margin-top: 10vh;">
        <el-option v-for="item in tasks" :key="item.id" :label="item.label" :value="item.value"></el-option>
      </el-select>
      <el-select v-model="ship" placeholder="请选择舰型" class="selectBg" label="舰型">
        <el-option v-for="item in ships" :key="item.id" :label="item.label" :value="item.value"></el-option>
      </el-select>
      <el-select v-model="plane" placeholder="请选择机型" class="selectBg">
        <el-option v-for="item in planes" :key="item.id" :label="item.label" :value="item.value"></el-option>
      </el-select>
      <el-select v-model="dqtx" placeholder="请选择通信载荷" class="selectBg">
        <el-option v-for="item in txzhs" :key="item.id" :label="item.label" :value="item.value"></el-option>
      </el-select>
      <el-select v-model="dqtc" placeholder="请选择探测载荷" class="selectBg">
        <el-option v-for="item in tczhs" :key="item.id" :label="item.label" :value="item.value"></el-option>
      </el-select>
      <el-select v-model="dqgj" placeholder="请选择攻击载荷" class="head">
        <el-option v-for="item in gjzhs" :key="item.id" :label="item.label" :value="item.value"></el-option>
      </el-select>
      <el-input class="input" v-model="dqfx" placeholder="请输入风向"></el-input>
      <el-input class="input" v-model="dqfs" placeholder="请输入风速"></el-input>
      <el-input class="input" v-model="dqydg" placeholder="请输入云底高"></el-input>
      <el-input class="input" v-model="dqnjd" placeholder="请输入能见度" style="margin-left: 3.4vw;"></el-input>
      <el-input class="input" v-model="dqdqwd" placeholder="请输入大气温度"></el-input>
      <el-input class="input" v-model="dqjsl" placeholder="请输入降水量"></el-input>
      <el-input class="input" v-model="dqdqbd" placeholder="请输入大气波导类型"></el-input>
      <el-input class="input" v-model="dqhk" placeholder="请输入海况" style="margin-left: 3.4vw;"></el-input>
      <el-input class="input" v-model="dqlx" placeholder="请输入流向"></el-input>
      <el-input class="input" v-model="dqls" placeholder="请输入流速"></el-input>
      <el-input class="input" v-model="dqhs" placeholder="请输入海深"></el-input>
      <el-button @click="getHistoryNew" type="primary" style="margin-left: 73vw;margin-bottom: 2vh;">检索</el-button>
      <div class="inputBg">
        <el-table :data="tableDataList" style="background-color: transparent;">
          <el-table-column prop="bgName" label="报告名称" header-align="center" align="center" style="color: #fff;">
          </el-table-column>
          <el-table-column prop="name" label="操作" header-align="center" align="center" style="color: #fff;">
            <template slot-scope="scope">
              <el-button size="mini" @click="lookInfo(scope.row)">编辑
              </el-button>
              <el-button size="mini" type="warning" @click="downLoadWord(scope.row)">下载
              </el-button>
              <el-button size="mini" type="danger" @click="delteInfo(scope.row)">删除
              </el-button>
            </template>
          </el-table-column>
        </el-table>
      </div>
    </el-dialog>


    <!--  计算结果选择  -->
    <el-dialog title="计算结果列表" :visible.sync="dialogVisibleJs" width="80%">


      <div v-if="this.jsType != 0">
        <el-button v-for="item in buttonList" :key="item" @click="changeJsType(item.type)">{{ item.text }}</el-button>
      </div>

      <el-table ref="myTable" :data="tableDataListJs" v-if="jsKey == 'QJFXT'">
        <el-table-column prop="M" label="云底高" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="N" label="能见度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Y" label="横摇角度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Z" label="纵摇角度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="A_mag" label="航速" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="A_dir" label="航向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="B_mag" label="风速" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="B_dir" label="风向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="C_dir_0" label="浪向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="T" label="纵摇周期" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="L" label="波长" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="ship_type" label="舰艇型号" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="heli_type" label="飞机型号" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="target_R_mag" label="期望风速" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="useZjsb" label="是否使用助降设备" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="zjsb" label="助降设备" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="A_adj_mag" label="调整后航速" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="A3" label="调整后航向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="VAll" label="谐振航速" header-align="center" align="center">

        </el-table-column>

        <el-table-column prop="R_1" label="合成风向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="R_mag" label="合成风速" header-align="center" align="center">
        </el-table-column>

        <el-table-column prop="tz" label="能否调整" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="yy" label="原因" header-align="center" align="center">
        </el-table-column>

        <el-table-column prop="allImg" label="图片" width="200" header-align="center" align="center">
          <template slot-scope="scope">
            <el-image style="width: 80px; height: 80px" :src="scope.row.allImg.split(',')[0]"
              :preview-src-list="[scope.row.allImg.split(',')[0]]" fit="cover" hide-on-click-modal></el-image>
          </template>

        </el-table-column>
        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>

      </el-table>
      <el-table ref="myTable" :data="tableDataListJs" v-if="jsKey == 'SN1'">
        <el-table-column prop="delta_depth" label="深度的间隔" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="z1" label="跃层之上的截止深度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="r2" label="距离上的初始最大值" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="delta_r" label="距离上的间隔" header-align="center" align="center">
        </el-table-column>

        <el-table-column prop="Nrd" label="接收器深度点数" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Nrr" label="固定接收器距离点数" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="num_points" label="固定点数" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="SeaDep" label="海底类型" header-align="center" align="center">
        </el-table-column>

        <el-table-column prop="sspm" label="声速剖面" header-align="center" align="center">
          <template v-slot="scope">
            <div>{{ scope.row.sspmText1 + '' + scope.row.sspmText2 }}</div>
          </template>
        </el-table-column>

        <el-table-column prop="bty" label="地形数据" header-align="center" align="center">
          <template v-slot="scope">
            <div>{{ scope.row.byt1 + '' + scope.row.byt2 }}</div>
          </template>
        </el-table-column>

        <el-table-column prop="freq" label="声源频率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Pos_s_depth" label="声源深度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Beam_Nbeams" label="声线数目" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="alpha" label="波束张开角度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Bdry_Bot_cp" label="底部声速" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Bdry_Bot_rho" label="底部密度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Bdry_Bot_rholns" label="底部衰减" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Bdry_Bot_cs" label="海底s波速度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="SL" label="声呐发射声源级" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="B" label="接收带宽" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="TT" label="积分时间" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="DI" label="DI" header-align="center" align="center">

        </el-table-column>

        <el-table-column prop="TS_alpha" label="目标强度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="S" label="海况等级" header-align="center" align="center">
        </el-table-column>

        <el-table-column prop="creatime" label="创建时间" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="allImg" label="图片" width="200" header-align="center" align="center">
          <template slot-scope="scope">
            <el-image style="width: 80px; height: 80px" :src="scope.row.allImg.split(',')[0]"
              :preview-src-list="[scope.row.allImg.split(',')[0]]" fit="cover" hide-on-click-modal></el-image>
            <el-image style="width: 80px; height: 80px" :src="scope.row.allImg.split(',')[1]"
              :preview-src-list="[scope.row.allImg.split(',')[0]]" fit="cover" hide-on-click-modal></el-image>
            <!--            <img-->
            <!--                style="width: 100px; height: 100px"-->
            <!--                :src="scope.row.allImg" />-->
          </template>

        </el-table-column>
        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>
      </el-table>


      <el-table ref="myTableTx1" :data="tableDataListJs" v-if="jsKey == 'DBDLC'">
        <el-table-column prop="a" label="方位角" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="b" label="发射仰角" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="longtitude" label="发射点经度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="latitude" label="发射点纬度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="fre" label="工作频率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="N_m" label="最大电子密度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="r_m" label="电离层最大高度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="r_b" label="电离层底部高度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="allImg" label="图片" width="200" header-align="center" align="center">
          <template slot-scope="scope">
            <el-image style="width: 80px; height: 80px" :src="scope.row.allImg" :preview-src-list="[scope.row.allImg]"
              fit="cover" hide-on-click-modal></el-image>
            <!--            <img-->
            <!--                style="width: 100px; height: 100px"-->
            <!--                :src="scope.row.allImg" />-->
          </template>

        </el-table-column>

        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>
      </el-table>


      <el-table ref="myTableTx1" :data="tableDataListJs" v-if="jsKey == 'CDBTX'">
        <el-table-column prop="H" label="飞机高度H(m)" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="D" label="表面波导厚度D(m)" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="F" label="超短波频率F(mHz)" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="answer" label="结果" header-align="center" align="center">
        </el-table-column>


        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>
      </el-table>

      <el-table ref="myTable" :data="tableDataListJs" v-if="jsKey == 'YLDQGJ'">
        <el-table-column prop="h_c0" label="直升机航向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="h_v" label="直升机航速 " header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="h_h" label="直升机高度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="yl_b" label="投雷方位" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="yl_d" label="投雷距离" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="t_zb" label="投雷延时" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="err_dx" label="投雷横向误差" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="err_dy" label="投雷纵向误差" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="yl_hc" label="鱼雷航程" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="v_yl" label="鱼雷速度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="h_yl" label="工作深度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="t_wdl" label="无动力时间" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="r_t" label="旋回半径" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="omiga_detle" label="角度变化率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="lamda" label="扇面半开角" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="sl" label="声源级" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="f" label="频率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="di" label="接收指向性指数" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="dt" label="检测阈值" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="yl_yinxin" label="鱼雷引信" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="qt_x00" label="潜艇初始位置x" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="qt_y00" label="潜艇初始位置y" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="qt_v0" label="潜艇航速" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="qt_h0" label="潜艇初始航向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="ts0" label="反射强度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="ylbg_jl" label="报警距离" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="qt_xh" label="机动速度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="flag_jidong" label="是否机动" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="sl_gr" label="辐射噪声级" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="gr_d" label="距离" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="dfjs_gr" label="辐射噪声宽度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="gr_q" label="舷角" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="df_gr" label="接收噪声宽度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="flag_ganraoqi" label="是否释放干扰器" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="delta_t" label="仿真时间" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="s_hk" label="海况" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="fz_num" label="仿真次数" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="result" label="命中概率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="resultStr" label="状态" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="finalHc" label="鱼雷航程" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="finalZD" label="声自导距离" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="createTime" label="创建时间" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="allImg" label="图片" width="200" header-align="center" align="center">
          <template slot-scope="scope">
            <el-image style="width: 80px; height: 80px" :src="scope.row.allImg" :preview-src-list="[scope.row.allImg]"
              fit="cover" hide-on-click-modal></el-image>
            <!--            <img-->
            <!--                style="width: 100px; height: 100px"-->
            <!--                :src="scope.row.allImg" />-->
          </template>

        </el-table-column>

        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>
        <!--            <el-table-column-->
        <!--                prop="address"-->
        <!--                label="地址">-->
        <!--            </el-table-column>-->
      </el-table>

      <el-table ref="myTable" :data="tableDataListJs" v-if="jsKey == 'DDZZSYFZJC'">
        <el-table-column prop="Hel_D" label="直升机距离" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Hel_B" label="直升机方位 " header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Hel_c0" label="直升机航向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Hel_v" label="直升机航速" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Hel_h" label="直升机高度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Err_theta" label="目标角度误差" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Err_D" label="目指距离误差" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="KT_x0" label="快艇初始x位置" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="KT_y0" label="快艇初始y位置" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="KT_v0" label="快艇航速" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="KT_H0" label="快艇航向" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="KT_DT_missle" label="导弹探测距离" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="KT_AT_hel" label="对空攻击距离" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="V_missle" label="空舰导弹速度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Mis_hc" label="空舰导弹距离" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Mis_sc" label="空舰导弹方位" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Mis_D_Lamda" label="搜索扇面" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Mis_D_Lamda_err" label="扇面误差" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Mis_D_bc" label="波段" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Sea_hk" label="海况等级" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="MM" label="降水量" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="delta_t" label="仿真步长" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="num_sumli" label="仿真次数" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="result" label="命中概率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="resultStr" label="状态" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="createTime" label="创建时间" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="allImg" label="图片" width="200" header-align="center" align="center">
          <template slot-scope="scope">
            <el-image style="width: 80px; height: 80px" :src="scope.row.allImg" :preview-src-list="[scope.row.allImg]"
              fit="cover" hide-on-click-modal></el-image>
            <!--            <img-->
            <!--                style="width: 100px; height: 100px"-->
            <!--                :src="scope.row.allImg" />-->
          </template>

        </el-table-column>

        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>
        <!--            <el-table-column-->
        <!--                prop="address"-->
        <!--                label="地址">-->
        <!--            </el-table-column>-->
      </el-table>


      <el-table ref="myTable" :data="tableDataListJs" v-if="jsKey == 'SNJS'">
        <el-table-column prop="Mode" label="Mode" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="NoiseLevel" label="NoiseLevel " header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="DirectivityIndex" label="DirectivityIndex" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="TargetStrength" label="TargetStrength" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Frequency" label="Frequency" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="FrequencyUnit" label="FrequencyUnit" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Depth" label="Depth" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="DepthUnit" label="DepthUnit" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="SourceLevel" label="SourceLevel" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="SNR" label="SNR" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Pd" label="Pd" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Pfa" label="Pfa" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="N" label="N" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="SwerlingCase" label="SwerlingCase" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="targetRange" label="targetRange" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="targetRangeUnit" label="targetRangeUnit" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="createTime" label="createTime" header-align="center" align="center">
        </el-table-column>


        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>
        <!--            <el-table-column-->
        <!--                prop="address"-->
        <!--                label="地址">-->
        <!--            </el-table-column>-->
      </el-table>
      <el-table ref="myTableTc1" :data="tableDataListJs" v-if="jsKey == 'DQJS'">
        <el-table-column prop="trans_pwr_radar" label="发射功率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="freq_radar" label="雷达频率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="pulse_width" label="雷达脉冲宽度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="GTDB_radar" label="发射机增益" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="GRDB_radar" label="接收机增益" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="GRDB_sl_radar" label="雷达旁瓣" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="noise_fig_radar" label="接收机噪声系数" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="loss_radar_dB" label="雷达系统损失" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="PRF" label="脉冲重复频率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="prob_det" label="探测概率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="prob_false_alarm" label="虚警概率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="BW_dop" label="多普勒滤波器带宽" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="BW_fa" label="频率捷变" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="Azimuth_bw" label="方位波束宽度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="az_rate" label="方位扫描速率" header-align="center" align="center">
        </el-table-column>

        <el-table-column prop="RCS" label="雷达散射面积" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="el_tgt_deg" label="目标高度" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="target_length" label="目标长度" header-align="center" align="center">
        </el-table-column>
        <el-table-column v-if="tableDataListJs.some(item => item.useType === 1)" prop="rain_fall" label="降雨量"
          header-align="center" align="center">
        </el-table-column>
        <el-table-column v-if="tableDataListJs.some(item => item.useType === 2)" prop="rain_fall" label="降雪量"
          header-align="center" align="center">
        </el-table-column>
        <el-table-column v-if="tableDataListJs.some(item => item.useType === 3)" prop="rain_fall" label="密度"
          header-align="center" align="center">
        </el-table-column>
        <el-table-column v-if="tableDataListJs.some(item => item.useType === 3)" prop="T" label="温度"
          header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="allImg" label="图片" width="200" header-align="center" align="center">
          <template slot-scope="scope">
            <el-image style="width: 80px; height: 80px" :src="scope.row.allImg" :preview-src-list="[scope.row.allImg]"
              fit="cover" hide-on-click-modal></el-image>
            <!--            <img-->
            <!--                style="width: 100px; height: 100px"-->
            <!--                :src="scope.row.allImg" />-->
          </template>

        </el-table-column>


        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>
        <!--            <el-table-column-->
        <!--                prop="address"-->
        <!--                label="地址">-->
        <!--            </el-table-column>-->
      </el-table>
      <el-table ref="myTable" :data="tableDataListJs" v-if="jsKey == 'JSGL'">
        <el-table-column prop="Level_hk" label="海况等级 (0~9)" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="P_l" label="导弹掠海飞行高度 " header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="P_h" label="击水概率" header-align="center" align="center">
        </el-table-column>
        <el-table-column prop="allImg" label="图片" width="200" header-align="center" align="center">
          <template slot-scope="scope">
            <el-image style="width: 80px; height: 80px" :src="scope.row.allImg" :preview-src-list="[scope.row.allImg]"
              fit="cover" hide-on-click-modal></el-image>
            <!--            <img-->
            <!--                style="width: 100px; height: 100px"-->
            <!--                :src="scope.row.allImg" />-->
          </template>

        </el-table-column>


        <el-table-column prop="name" label="操作" header-align="center" fixed="right" align="center">
          <template slot-scope="scope">
            <el-button size="mini" @click="useInfo(scope.row)">使用
            </el-button>

          </template>
        </el-table-column>
        <!--            <el-table-column-->
        <!--                prop="address"-->
        <!--                label="地址">-->
        <!--            </el-table-column>-->
      </el-table>
    </el-dialog>

    <el-dialog title="XXXX辅助决策" :visible.sync="showQjJs" width="80%">
      <QJFXT :jsId="jsId"></QJFXT>
    </el-dialog>

    <el-dialog title="大气环境对雷达探测的影响分析软件" :visible.sync="showDQJs" width="80%">
      <DQJS :jsId="jsId"></DQJS>
    </el-dialog>

    <el-dialog title="声呐探测距离估算软件" :visible.sync="showSNJs" width="80%">
      <SNJS :jsId="jsId"></SNJS>
    </el-dialog>
    <!--    -->
    <el-dialog title="海洋环境对声呐探测的影响分析软件" :visible.sync="showSN1Js" width="80%">
      <SN1 :jsId="jsId"></SN1>
    </el-dialog>

    <!-- <el-dialog title="击水概率" :visible.sync="showJSJs" width="80%">
      <JSGL :jsId="jsId"></JSGL>
    </el-dialog> -->

    <el-dialog title="电离层对短波通信的影响分析软件" :visible.sync="showDBJs" width="80%">
      <DBDLC :jsId="jsId"></DBDLC>
    </el-dialog>

    <el-dialog title="舰载直升机航空鱼雷作战使用辅助决策软件" :visible.sync="showYLJs" width="80%">
      <YLDQGJ :jsId="jsId"></YLDQGJ>
    </el-dialog>

    <el-dialog title="舰载直升机空舰导弹作战使用辅助决策软件" :visible.sync="showDDZZJs" width="80%">
      <DDZZSYFZJC :jsId="jsId"></DDZZSYFZJC>
    </el-dialog>

    <el-dialog title="大气波导对电磁场传播的影响分析软件" :visible.sync="showLDJS" width="80%">
      <LDWLT :jsId="jsId"></LDWLT>
    </el-dialog>


    <el-dialog title="面向舰机超短波通信的表面波导可用性评估软件" :visible.sync="showCDBJS" width="80%">
      <CDBTX :jsId="jsId"></CDBTX>
    </el-dialog>

    <div style="width: 100%;height: 3%;position: fixed;bottom: 0px;z-index: 100">
      <foot></foot>
    </div>
  </div>

</template>
<style src="@wangeditor/editor/dist/css/style.css"></style>
<script>
import QJFXT from '@/view/jsXqs/QJFXTCopy.vue';
import DQJS from "@/view/jsXqs/DQJSCopy.vue";
import SNJS from '@/view/jsXqs/SNJSCopy.vue';
import SN1 from '@/view/jsXqs/SN1Copy.vue';
// import JSGL from '@/view/jsXqs/JSGLCopy.vue';
import DBDLC from '@/view/jsXqs/DBDLCCopy.vue';
import CDBTX from '@/view/jsXqs/CDBTXCopy.vue';
import YLDQGJ from "./jsXqs/YLDQGJCopy.vue";
import LDWLT from "./jsXqs/LDWLTCopy.vue";
import DDZZSYFZJC from "./jsXqs/DDZZSYFZJCCopy.vue";
import { Editor, Toolbar } from '@wangeditor/editor-for-vue'
import headInfo from "@/components/Head.vue";
import Foot from "@/components/Foot.vue";
import { config } from "@/assets/defaultConfig";
import VisGraph from '@/assets/js/graphvis.min.20241008.js'
import LayoutFactory from '@/assets/js/graphvis.layout.min.js'
import { getDomainGraphNew1 } from "@/api/login";
import { getJsList } from "@/api/kcInfo";
import { getFileIdData1 } from "@/api/export";
import { uploadAndExecuteSql1 } from "@/api/file";
import {
  editBaoGao,
  editTable,
  getAllHistory, getGz, insertGz,
  getTableComlun,
  getTableList,
  insertBaoGao,
  insertTable
} from "@/api/baogao";
import axios from "axios";
import { getToken } from "@/utils/auth";
import { getAllJsResult } from "@/api/jsJg";
import { fileUpdate } from "@/api/file";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'BoaGao',
  components: { Foot, headInfo, Editor, Toolbar, QJFXT, DQJS, SNJS, SN1, DBDLC, YLDQGJ, DDZZSYFZJC, LDWLT, CDBTX },
  data() {
    return {
      tczhysIndex: 0,
      editor: null,
      zzhjys: '<p>请输入起降环境因素</p>',
      zzhjys1: '<p>请输入起降环境因素</p>',
      fxhjys: '<p>请输入飞行作战环境因素</p>',
      fxhjys1: '<p>请输入飞行作战环境因素</p>',
      txzhys: '<p>请输入环境对通信载荷的影响</p>',
      txzhys1: '<p>请输入环境对通信载荷的影响</p>',
      tczhys: '<p>请输入环境对探测载荷的影响</p>',
      tczhys1: '<p>请输入环境对探测载荷的影响</p>',
      gjzhys: '<p>请输入环境对攻击载荷的影响</p>',
      gjzhys1: '<p>请输入环境对攻击载荷的影响</p>',
      isQjjs: false,
      isFxjs: false,
      isTcjs: false,
      isTxjs: false,
      isGjjs: false,
      options1: [{
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
      options2: [{
        value: '驱052D',
        label: '驱052D'
      }, {
        value: '护054D',
        label: '护054D'
      }, {
        value: '驱055',
        label: '驱055'
      }],
      options3: [{
        value: '直9D',
        label: '直9D'
      },
      {
        value: '直9F',
        label: '直9F'
      },
      {
        value: '直20',
        label: '直20'
      },
      {
        value: '卡28',
        label: '卡28'
      }],
      options4: [{
        value: '短波',
        label: '短波'
      },
      {
        value: '超短波',
        label: '超短波'
      }],
      options5: [{
        value: '机载雷达',
        label: '机载雷达'
      },
      {
        value: '吊放声呐',
        label: '吊放声呐'
      },
      {
        value: '声呐浮标',
        label: '声呐浮标'
      },
      {
        value: '光电探头',
        label: '光电探头'
      },
      {
        value: '磁探仪',
        label: '磁探仪'
      }],
      options6: [{
        value: '航空导弹',
        label: '航空导弹'
      },
      {
        value: '航空鱼雷',
        label: '航空鱼雷'
      }],
      task: "",
      ship: "",
      plane: "",
      dqtx: "",
      dqtc: "",
      dqgj: "",
      dqfx: "",
      dqfs: "",
      dqydg: "",
      dqnjd: "",
      dqdqwd: "",
      dqjsl: "",
      dqdqbd: "",
      dqhk: "",
      dqlx: "",
      dqls: "",
      dqhs: "",
      tasks: [{
        id: 1,
        label: "对潜攻击",
        value: "对潜攻击"
      },
      {
        id: 2,
        label: "对潜搜索",
        value: "对潜搜索"
      },
      {
        id: 3,
        label: "对海攻击",
        value: "对海攻击"
      },
      {
        id: 4,
        label: "预警侦察",
        value: "预警侦察"
      }],
      ships: [{
        id: 1,
        label: "护054A",
        value: "护054A"
      },
      {
        id: 2,
        label: "驱052D",
        value: "驱052D"
      },
      {
        id: 3,
        label: "驱055",
        value: "驱055"
      }],
      planes: [{
        id: 1,
        label: "直9D",
        value: "直9D"
      },
      {
        id: 2,
        label: "直9F",
        value: "直9F"
      },
      {
        id: 3,
        label: "卡28",
        value: "卡28"
      },
      {
        id: 4,
        label: "直20",
        value: "直20"
      }],
      txzhs: [{
        id: 1,
        label: "短波",
        value: "短波"
      },
      {
        id: 2,
        label: "超短波",
        value: "超短波"
      }],
      tczhs: [{
        id: 1,
        label: "机载雷达",
        value: "机载雷达"
      },
      {
        id: 2,
        label: "吊放声呐",
        value: "吊放声呐"
      },
      {
        id: 3,
        label: "声呐浮标",
        value: "声呐浮标"
      },
      {
        id: 4,
        label: "光电探头",
        value: "光电探头"
      },
      {
        id: 5,
        label: "磁探仪",
        value: "磁探仪"
      }],
      gjzhs: [{
        id: 1,
        label: "航空鱼雷",
        value: "航空鱼雷"
      },
      {
        id: 2,
        label: "航空导弹",
        value: "航空导弹"
      }],
      editorConfig1: {
        placeholder: '请输入作战环境因素',
        // 设置为只读模式
        readOnly: true,
        // 禁用所有菜单
        menus: []
      },
      editorConfig2: {
        placeholder: '请输入飞行作战环境因素',
        // 设置为只读模式
        readOnly: true,
        // 禁用所有菜单
        menus: []
      },
      editorConfig3: {
        placeholder: '请输入环境对通信载荷的影响',
        // 设置为只读模式
        readOnly: true,
        // 禁用所有菜单
        menus: []
      },
      editorConfig4: {
        placeholder: '请输入环境对探测载荷的影响',
        // 设置为只读模式
        readOnly: true,
        // 禁用所有菜单
        menus: []
      },
      editorConfig5: {
        placeholder: '请输入环境对攻击载荷的影响',
        // 设置为只读模式
        readOnly: true,
        // 禁用所有菜单
        menus: []
      },
      html: '<p>请输入规则内容</p>',
      toolbarConfig: {},
      editorConfig: {
        placeholder: '请输入内容...',
        // 所有的菜单配置，都要在 MENU_CONF 属性下
        MENU_CONF: {
          uploadImage: {
            // 图片文件上传接口地址
            server: 'http://127.0.0.1:10035/fileUpdate/upload',
            timeout: 5 * 1000, // 5s
            // fieldName 要与接口规定的Form Data文件字段名一致
            fieldName: 'file',
            maxFileSize: 10 * 1024 * 1024, // 10M
            // 若接口返回的数据结构与官方规定的不一致, 则需要 customInsert 方法将返回的路径传给编辑器
            customInsert(res, insertFn) {
              const url = res.data.url;
              insertFn(url)
            },
          },
        },
      },
      // const image = res.data.url;
      //         this.$axios({
      //           // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
      //           url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
      //           method: "get",//get请求方式
      //           params: { image },
      //           headers: {
      //             'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
      //             'Access-Control-Request-Method': 'GET',
      //             'Access-Control-Request-Headers': 'content-type',
      //           },
      //         }).then((res) => {
      //           console.log(res)

      //         })
      mode: 'default',
      showList: false,
      gzlist: [],
      showYun: false,
      yunlist: [],
      showNJD: false,
      njdlist: [],
      showFeng: false,
      fenglist: [],
      showQW: false,
      qwlist: [],
      showFJJB: false,
      fjjblist: [],
      showJYY: false,
      jyylist: [],
      showCDB: false,
      cdblist: [],
      showDB: false,
      dblist: [],
      showTCJL: false,
      tcjllist: [],
      showDQSJ: false,
      dqsjlist: [],
      showHZB: false,
      hzblist: [],
      showSSPM: false,
      sspmlist: [],
      showHK: false,
      hklist: [],
      showHL: false,
      hllist: [],
      showNB: false,
      nblist: [],
      showHYF: false,
      hyflist: [],
      showZCDW: false,
      zcdwlist: [],
      showKZXLD: false,
      kzxldlist: [],
      showXQXSD: false,
      xqxsdlist: [],
      showSSD: false,
      ssdlist: [],
      showGZD: false,
      gzdlist: [],
      showZSJTF: false,
      zsjtflist: [],
      showDDDD: false,
      ddddlist: [],
      showDDMZD: false,
      ddmzdlist: [],
      jtxh: {
        text: "请选择舰型"
      },
      fjxh: {
        text: "请选择机型"
      },
      txzh: {
        text: "请选择通信载荷"
      },
      tczh: {
        text: "请选择探测载荷"
      },
      gjzh: {
        text: "请选择攻击载荷"
      },
      selectedOption6: null,
      // 侧边栏状态
      sidebarVisible: false,
      // 侧边栏项目
      sidebarItems: [
        "起降",
        "飞行",
        "探测",
        "通信",
        "攻击"
      ],
      editorOptions: {
        modules: {
          toolbar: [
            ['bold', 'italic', 'underline', 'strike'], // 格式化工具
            ['blockquote', 'code-block'], // 引用和代码块
            [{ header: 1 }, { header: 2 }], // 标题
            [{ list: 'ordered' }, { list: 'bullet' }], // 列表
            [{ script: 'sub' }, { script: 'super' }], // 上标和下标
            [{ indent: '-1' }, { indent: '+1' }], // 缩进
            [{ direction: 'rtl' }], // 文本方向
            [{ size: ['small', false, 'large', 'huge'] }], // 字体大小
            [{ header: [1, 2, 3, 4, 5, 6, false] }], // 标题
            [{ font: [] }], // 字体
            [{ color: [] }, { background: [] }], // 字体颜色和背景颜色
            [{ align: [] }], // 对齐方式
            ['clean'], // 清除格式
            ['link', 'image', 'video'] // 链接、图片、视频
          ]
        }
      },
      gzType: undefined,
      gzwenben: undefined,
      gzText: {
        image: undefined,
        text: undefined,
      },
      gzInfoType: undefined,
      gzInfoType1: undefined,
      gzTypeList: [
        {
          id: 1,
          label: "起降",
          value: "起降",
        },
        {
          id: 2,
          label: "飞行",
          value: "飞行",
        },
        {
          id: 3,
          label: "探测",
          value: "探测",
        },
        {
          id: 4,
          label: "通信",
          value: "通信",
        },
        {
          id: 5,
          label: "攻击",
          value: "攻击",
        },
      ],
      yjgzTypeList: [],
      ejgzTypeList: [],
      qjjslist: [],
      fxjslist: [],
      txjslist: [],
      tcjslist: [],
      gjjslist: [],
      selectedSidebarItem: null,

      //计算结果列表
      dialogVisibleJs: false,
      tableDataListJs: [],
      jsKey: "CDBTX",
      jsType: 0,
      buttonList: [],


      //列表管理数据
      lieBiaoList: [],
      showLieBiao: false,
      showEdit: false,
      comlunName: "",
      comlunkey: "",
      comlunId: undefined,


      baoGaoName: "",
      dialogVisibleInput: false,
      //弹窗数据
      dialogTableVisible: false,
      form: {
        propName: '',
      },
      form1: {
        "type": "",
        "plane": [],
        "info": {
          "info1": [],
          "info2": [],
        }
      },
      formLabelWidth: '120px',


      //起降图谱数据
      demoData: {},
      graphData: {
        nodes: [],
        links: []
      },

      //飞行图谱数据
      demoData1: {},
      graphData1: {
        nodes: [],
        links: []
      },
      indexNum: 0,

      //通信载荷图谱数据
      demoData2: {},
      graphData2: {
        nodes: [],
        links: []
      },


      //探测载荷图谱数据
      demoData3: {},
      graphData3: {
        nodes: [],
        links: []
      },


      //攻击载荷图谱数据
      demoData4: {},
      graphData4: {
        nodes: [],
        links: []
      },
      tableDataList: [],
      dialogVisibleList: false,

      config,
      visGraph: null, // 组件中保存VisGraph实例
      visGraph1: null, // 组件中保存VisGraph实例
      visGraph2: null, // 组件中保存VisGraph实例
      visGraph3: null, // 组件中保存VisGraph实例
      visGraph4: null, // 组件中保存VisGraph实例

      userName: "",
      currentDialog: '',
      mulu: [
        { id: 0, name: "知识图谱", info: "Graph" },
        { id: 1, name: "辅助决策", info: "BaoGao" },
        { id: 2, name: "图文资源", info: "TwInfo" },
        { id: 3, name: "视频资源", info: "SpInfo" },
        { id: 4, name: "动画显示", info: "DhInfo" },
        { id: 5, name: "数值计算", info: "JsInfo" },
        { id: 6, name: "帮助文档", info: "HelpInfo" }
      ],
      // keywords: "寒潮",
      // keywords1: "台风",
      // keywords2: "冰雹",
      // keywords3: "雷暴",
      // keywords4: "天气图",
      jsId: null,
      rwmc: {
        text: "请选择任务"
      },
      rwmd: "",
      rwsj: "",
      rwhj: [
        {
          firstRow: {
            name: '某海域',
            no: '1',
            bz: '无',
            fx: 10,
            fs: 3,
            njd: 30,
            yg: 1000
          },
          secondRow: {
            dqwd: 0,
            jsl: 0,
            dqbd: 0,
            hk: 0,
            lx: 0,
            ls: 0,
            hs: 0
          }
        }],
      dynamicColumns: [
        { prop: 'name', label: '名称' },
        { prop: 'no', label: '编号' },
        { prop: 'bz', label: '备注' },
        { prop: 'fx', label: '风向' },
        { prop: 'fs', label: '风速' },
        { prop: 'njd', label: '能见度' },
        { prop: 'yg', label: '云高' },
      ],
      dynamicColumns1: [
        { prop: 'dqwd', label: '大气温度' },
        { prop: 'jsl', label: '降水量' },
        { prop: 'dqbd', label: '大气波导' },
        { prop: 'hk', label: '海况' },
        { prop: 'lx', label: '流向' },
        { prop: 'ls', label: '流速' },
        { prop: 'hs', label: '海深' }
      ],


      jtbl: [{
        xvhao: 1,
        lx: "",
        xinghao: "",
        xjh: "",
        ms: "",
        bz: "",

      }],
      zsjbl: [
        {
          xvhao: 1,
          lx: "舰载直升机",
          xh: "",
          xjh: "",
          ms: "",
          bz: ""
        },
      ],
      rwhq: "",
      showDDZZJs: false,
      showLDJS: false,
      showYLJs: false,
      showDBJs: false,
      showJSJs: false,
      showSN1Js: false,
      showSNJs: false,
      showDQJs: false,
      showQjJs: false,
      showCDBJS: false,
      showTp1: false,

      bkSrc: require("@/assets/img/bkbg.png"),

      qjtp: '',
      // zzhjys: "",
      jzhjys: "",
      qjysImg: "",
      fxtp: '',
      // fxhjys: "",
      txtp: '',
      // txzhys: "",
      txzhysImg: "",
      tctp: '',
      // tczhys: "",
      tczhysImg: "",
      tczhysImg1: "",
      gjtp: '',
      // gjzhys: "",
      gjzhysImg: "",


      // txzh: [{
      //   txfs: "短波",
      //   txzb: "",
      //   bz: ""
      // },
      // {
      //   txfs: "",
      //   txzb: "",
      //   bz: ""
      // },
      // ],

      // tczh: [{
      //   tcsb: "",
      //   tczb: "",
      //   bz: ""
      // },
      // {
      //   tcsb: "",
      //   tczb: "",
      //   bz: ""
      // },
      // {
      //   tcsb: "",
      //   tczb: "",
      //   bz: ""
      // },
      // ],


      // gjzh: [{
      //   wqlx: "",
      //   wqzb: "",
      //   bz: ""
      // },
      // {
      //   wqlx: "",
      //   wqzb: "",
      //   bz: ""
      // },
      // {
      //   wqlx: "",
      //   wqzb: "",
      //   bz: ""
      // },
      // ],

      showGz: false,
      showTp2: false,
      showTp3: false,
      showTp4: false,
      showTp5: false,
      showOptions1: false,
      showOptions2: false,
      showOptions3: false,
      showOptions4: false,
      showOptions5: false,
      typePic1: 0,
      typePic2: 0,
      typePic3: 0,
      typePic4: 0,
      typePic5: 0,
      typePic6: 0,
      allTable: [],

      allExportList: [],
      hjys: {
        tableTitle: "环境因素",
        headers: ["海域", "编号", "能见度", "云高", "风向", "风速"],
        rows: [
          ["海域1", 1, 300, 400, 500, 12],
          ["海域2", 2, 500, 200, 200, 12],
          ["海域3", 3, 700, 300, 500, 12],
          ["海域4", 4, 900, 500, 300, 12]
          // 可以动态添加更多行
        ],

      },
      jt: {
        tableTitle: "舰艇兵力",
        headers: ["序号", "类型", "型号", "舷(机)号", "描述", "备注"],
        rows: [],
      },
      zsj: {
        tableTitle: "舰载直升机",
        headers: ["序号", "类型", "型号", "舷(机)号", "描述", "备注"],
        rows: [],
      },
      tx: {
        tableTitle: "通信载荷",
        headers: ["通信方式", "通信装备", "备注"],
        rows: [],
      },
      tc: {
        tableTitle: "探测载荷",
        headers: ["探测设备", "探测装备", "备注"],
        rows: [],
      },
      gj: {
        tableTitle: "攻击载荷",
        headers: ["武器类型", "武器装备", "备注"],
        rows: [],
      },
      bgId: undefined,
      resultJson: null,
      ImgG: "",


    }
  },

  methods: {
    openDialog() {
      this.dialogVisibleList = true;
      this.getHistoryNew()
    },
    handleFileChangeData(event) {
      const file = event.target.files[0]; // 确保文件已选择
      if (file) {
        this.uploadData(file);
      }
    },
    showGJZH() {
      return this.rwmc.text !== '对潜搜索' && this.rwmc.text !== '预警侦察';
    },
    uploadData(file) {
      uploadAndExecuteSql1(file)
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
          this.$refs.fileInputData.value = null;
        });
    },
    openFileInputData() {
      console.log(this.$refs)
      // this.editBaoGao = false;
      this.$refs.fileInputData.click();
    },
    exportSql() {
      getFileIdData1();
    },
    selectOption1(option) {
      this.rwmc = option;
      this.rwmc.text = option.label;
      this.searchTuPu()
    },
    selectOption2(option) {
      this.jtxh = option;
      this.jtxh.text = option.label;
      if ((this.rwmc.text == "对潜攻击" || this.rwmc.text == "对潜搜索") && (this.jtxh.text == "驱052D" || this.jtxh.text == "护054A")) {
        this.options3 = [{
          value: '直9F',
          label: '直9F'
        },
        {
          value: '卡28',
          label: '卡28'
        }]
      } else if ((this.rwmc.text == "对潜攻击" || this.rwmc.text == "对潜搜索") && this.jtxh.text == "驱055") {
        this.options3 = [{
          value: '直9F',
          label: '直9F'
        },
        {
          value: '直20',
          label: '直20'
        }]
      } else if (this.rwmc.text == "对海攻击（反舰）" && (this.jtxh.text == "驱052D" || this.jtxh.text == "护054A")) {
        this.options3 = [{
          value: '直9D',
          label: '直9D'
        }]
      } else if (this.rwmc.text == "对海攻击（反舰）" && this.jtxh.text == "驱055") {
        this.options3 = [{
          value: '直9D',
          label: '直9D'
        },
        {
          value: '直20',
          label: '直20'
        }]
      } else if (this.rwmc.text == "预警侦查" && (this.jtxh.text == "驱052D" || this.jtxh.text == "护054A")) {
        this.options3 = [{
          value: '直9D',
          label: '直9D'
        },
        {
          value: '直9F',
          label: '直9F'
        },
        {
          value: '卡28',
          label: '卡28'
        }]
      } else if (this.rwmc.text == "预警侦查" && this.jtxh.text == "驱055") {
        this.options3 = [{
          value: '直9D',
          label: '直9D'
        },
        {
          value: '直9F',
          label: '直9F'
        },
        {
          value: '直20',
          label: '直20'
        }]
      }
    },
    selectOption3(option) {
      this.fjxh = option;
      this.fjxh.text = option.label;
      if (this.rwmc.text == "对潜攻击") {
        this.options5 = [{
          value: '机载雷达',
          label: '机载雷达'
        }]
        this.options6 = [{
          value: '航空鱼雷',
          label: '航空鱼雷'
        }]
      }
      if (this.rwmc.text == "对潜搜索") {
        if (this.fjxh.text == "直20" || this.fjxh.text == "卡28") {
          this.options5 = [{
            value: '机载雷达',
            label: '机载雷达'
          },
          {
            value: '吊放声呐',
            label: '吊放声呐'
          },
          {
            value: '声呐浮标',
            label: '声呐浮标'
          }]
          this.options6 = []
        }
        if (this.fjxh.text == "直9F") {
          this.options5 = [{
            value: '机载雷达',
            label: '机载雷达'
          },
          {
            value: '吊放声呐',
            label: '吊放声呐'
          }]
          this.options6 = []
        }
      }
      if (this.rwmc.text == "对海攻击（反舰）") {
        this.options5 = [{
          value: '机载雷达',
          label: '机载雷达'
        },
        {
          value: '光电探头',
          label: '光电探头'
        }]
        this.options6 = [{
          value: '航空导弹',
          label: '航空导弹'
        }]
      }
      if (this.rwmc.text == "预警侦察") {
        this.options5 = [{
          value: '机载雷达',
          label: '机载雷达'
        }]
        this.options6 = []
      }
      this.searchTuPu();
    },
    selectOption4(option) {
      this.txzh = option;
      this.txzh.text = option.label;
      this.searchTuPu();
    },
    selectOption5(option) {
      this.tczh = option;
      this.tczh.text = option.label;
      this.searchTuPu();
    },
    selectOption6(option) {
      this.gjzh = option;
      this.gjzh.text = option.label;
      this.searchTuPu();
    },
    toggleOptions1() {
      if (this.typePic1 == 0) {
        this.typePic1 = 1;
      } else {
        this.typePic1 = 0;
      }
      this.showOptions1 = !this.showOptions1;
    },
    toggleOptions2() {
      if (this.typePic2 == 0) {
        this.typePic2 = 1;
      } else {
        this.typePic2 = 0;
      }
      this.showOptions2 = !this.showOptions2;
    },
    toggleOptions3() {
      if (this.typePic3 == 0) {
        this.typePic3 = 1;
      } else {
        this.typePic3 = 0;
      }
      this.showOptions3 = !this.showOptions3;
    },
    toggleOptions4() {
      if (this.typePic4 == 0) {
        this.typePic4 = 1;
      } else {
        this.typePic4 = 0;
      }
      this.showOptions4 = !this.showOptions4;
    },
    toggleOptions5() {
      if (this.typePic5 == 0) {
        this.typePic5 = 1;
      } else {
        this.typePic5 = 0;
      }
      this.showOptions5 = !this.showOptions5;
    },
    toggleOptions6() {
      if (this.typePic6 == 0) {
        this.typePic6 = 1;
      } else {
        this.typePic6 = 0;
      }
      this.showOptions6 = !this.showOptions6;
    },
    onCreated(editor) {
      this.editor = Object.seal(editor) // 一定要用 Object.seal() ，否则会报错
    },
    useGz(row) {
      console.log(row.text);
      if (row.type == "起降") {
        var ps1 = row.text.split("<br>");
        // this.zzhjys = `<p>${row.text}</p>`;
        const results = [];
        for (let i = 0; i < ps1.length; i++) {
          if (ps1[i] !== '' && ps1[i] !== undefined) {
            if (this.zzhjys == "<p>请输入起降环境因素</p>") {
              this.zzhjys = `<p>${ps1[i]}</p>`
            } else {
              const newContent = `<p>${ps1[i]}</p>`;
              this.zzhjys = this.zzhjys + newContent;
            }
          }
          let result = [];
          if (ps1[i] !== '' && ps1[i] !== undefined) {
            let str = ps1[i];
            if (str.includes("img")) {
              const imgRegex = /<img[^>]*>/g;
              const textRegex = /,([^<]+),/g;
              let str1 = str;
              const matches = Array.from(str1.matchAll(imgRegex));
              for (const match of matches) {
                str1 = str1.replace(match[0], ",");
                result.push(match[0]);
              }
              const matches1 = Array.from(str1.matchAll(textRegex));
              for (const match of matches1) {
                str1 = str1.replace(match[1], ",");
                result.push(match[1]);
              }
              let strs = str1.split(",");
              for (let index = 0; index < strs.length; index++) {
                if (strs[index] !== "" && strs[index] !== undefined) {
                  result.push(strs[index])
                }
              }
              result.sort((a, b) => {
                const aIndex = str.indexOf(a);
                const bIndex = str.indexOf(b);
                return aIndex - bIndex;
              });
              console.log(result)
              let str2 = result.join(",") + "<br>";
              // console.log(results)
              results.push(str2)
            } else {
              results.push(str + "<br>")
            }
          }
        }
        this.zzhjys1 = results.join(",")
      }
      if (row.type == "飞行") {
        var ps2 = row.text.split("<br>");
        // this.zzhjys = `<p>${row.text}</p>`;
        const results = [];
        for (let i = 0; i < ps2.length; i++) {
          if (ps2[i] !== '' && ps2[i] !== undefined) {
            if (this.fxhjys == "<p>请输入飞行作战环境因素</p>") {
              this.fxhjys = `<p>${ps2[i]}</p>`
            } else {
              const newContent = `<p>${ps2[i]}</p>`;
              this.fxhjys = this.fxhjys + newContent;
            }
          }
          let result = [];
          if (ps2[i] !== '' && ps2[i] !== undefined) {
            let str = ps2[i];
            if (str.includes("img")) {
              const imgRegex = /<img[^>]*>/g;
              const textRegex = /,([^<]+),/g;
              let str1 = str;
              const matches = Array.from(str1.matchAll(imgRegex));
              for (const match of matches) {
                str1 = str1.replace(match[0], ",");
                result.push(match[0]);
              }
              const matches1 = Array.from(str1.matchAll(textRegex));
              for (const match of matches1) {
                str1 = str1.replace(match[1], ",");
                result.push(match[1]);
              }
              let strs = str1.split(",");
              for (let index = 0; index < strs.length; index++) {
                if (strs[index] !== "" && strs[index] !== undefined) {
                  result.push(strs[index])
                }
              }
              result.sort((a, b) => {
                const aIndex = str.indexOf(a);
                const bIndex = str.indexOf(b);
                return aIndex - bIndex;
              });
              console.log(result)
              let str2 = result.join(",") + "<br>";
              console.log(str2)
              results.push(str2)
            } else {
              results.push(str + "<br>")
            }
          }
        }
        console.log(results);
        this.fxhjys1 = results.join(",")
        console.log(this.fxhjys1)
        // if (this.fxhjys == "<p>请输入飞行作战环境因素</p>") {
        //   this.fxhjys = `<p>${row.text}</p>`;
        // } else {
        //   const newContent = `<p>${row.text}</p>`;
        //   this.fxhjys = this.fxhjys + ";" + newContent;
        // }
      }
      if (row.type == "通信") {
        var ps3 = row.text.split("<br>");
        // this.zzhjys = `<p>${row.text}</p>`;
        const results = [];
        for (let i = 0; i < ps3.length; i++) {
          if (ps3[i] !== '' && ps3[i] !== undefined) {
            if (this.txzhys == "<p>请输入环境对通信载荷的影响</p>") {
              this.txzhys = `<p>${ps3[i]}</p>`
            } else {
              const newContent = `<p>${ps3[i]}</p>`;
              this.txzhys = this.txzhys + newContent;
            }
          }
          let result = [];
          if (ps3[i] !== '' && ps3[i] !== undefined) {
            let str = ps3[i];
            if (str.includes("img")) {
              const imgRegex = /<img[^>]*>/g;
              const textRegex = /,([^<]+),/g;
              let str1 = str;
              const matches = Array.from(str1.matchAll(imgRegex));
              for (const match of matches) {
                str1 = str1.replace(match[0], ",");
                result.push(match[0]);
              }
              const matches1 = Array.from(str1.matchAll(textRegex));
              for (const match of matches1) {
                str1 = str1.replace(match[1], ",");
                result.push(match[1]);
              }
              let strs = str1.split(",");
              for (let index = 0; index < strs.length; index++) {
                if (strs[index] !== "" && strs[index] !== undefined) {
                  result.push(strs[index])
                }
              }
              result.sort((a, b) => {
                const aIndex = str.indexOf(a);
                const bIndex = str.indexOf(b);
                return aIndex - bIndex;
              });
              console.log(result)
              let str2 = result.join(",") + "<br>";
              console.log(str2)
              results.push(str2)
            } else {
              results.push(str + "<br>")
            }
          }
        }
        console.log(results);
        this.txzhys1 = results.join(",")
        console.log(this.txzhys1)
      }
      if (row.type == "探测") {
        var ps4 = row.text.split("<br>");
        // this.zzhjys = `<p>${row.text}</p>`;
        const results = [];
        for (let i = 0; i < ps4.length; i++) {
          if (ps4[i] !== '' && ps4[i] !== undefined) {
            if (this.tczhys == "<p>请输入环境对探测载荷的影响</p>") {
              this.tczhys = `<p>${ps4[i]}</p>`
            } else {
              const newContent = `<p>${ps4[i]}</p>`;
              this.tczhys = this.tczhys + newContent;
            }
          }
          let result = [];
          if (ps4[i] !== '' && ps4[i] !== undefined) {
            let str = ps4[i];
            if (str.includes("img")) {
              const imgRegex = /<img[^>]*>/g;
              const textRegex = /,([^<]+),/g;
              let str1 = str;
              const matches = Array.from(str1.matchAll(imgRegex));
              for (const match of matches) {
                str1 = str1.replace(match[0], ",");
                result.push(match[0]);
              }
              const matches1 = Array.from(str1.matchAll(textRegex));
              for (const match of matches1) {
                str1 = str1.replace(match[1], ",");
                result.push(match[1]);
              }
              let strs = str1.split(",");
              for (let index = 0; index < strs.length; index++) {
                if (strs[index] !== "" && strs[index] !== undefined) {
                  result.push(strs[index])
                }
              }
              result.sort((a, b) => {
                const aIndex = str.indexOf(a);
                const bIndex = str.indexOf(b);
                return aIndex - bIndex;
              });
              console.log(result)
              let str2 = result.join(",") + "<br>";
              console.log(str2)
              results.push(str2)
            } else {
              results.push(str + "<br>")
            }
          }
        }
        console.log(results);
        this.tczhys1 = results.join(",")
        console.log(this.tczhys1)
      }
      if (row.type == "攻击") {
        var ps5 = row.text.split("<br>");
        // this.zzhjys = `<p>${row.text}</p>`;
        const results = [];
        for (let i = 0; i < ps5.length; i++) {
          if (ps5[i] !== '' && ps5[i] !== undefined) {
            if (this.gjzhys == "<p>请输入环境对攻击载荷的影响</p>") {
              this.gjzhys = `<p>${ps5[i]}</p>`
            } else {
              const newContent = `<p>${ps5[i]}</p>`;
              this.gjzhys = this.gjzhys + newContent;
            }
          }
          let result = [];
          if (ps5[i] !== '' && ps5[i] !== undefined) {
            let str = ps5[i];
            if (str.includes("img")) {
              const imgRegex = /<img[^>]*>/g;
              const textRegex = /,([^<]+),/g;
              let str1 = str;
              const matches = Array.from(str1.matchAll(imgRegex));
              for (const match of matches) {
                str1 = str1.replace(match[0], ",");
                result.push(match[0]);
              }
              const matches1 = Array.from(str1.matchAll(textRegex));
              for (const match of matches1) {
                str1 = str1.replace(match[1], ",");
                result.push(match[1]);
              }
              let strs = str1.split(",");
              for (let index = 0; index < strs.length; index++) {
                if (strs[index] !== "" && strs[index] !== undefined) {
                  result.push(strs[index])
                }
              }
              result.sort((a, b) => {
                const aIndex = str.indexOf(a);
                const bIndex = str.indexOf(b);
                return aIndex - bIndex;
              });
              console.log(result)
              let str2 = result.join(",") + "<br>";
              console.log(str2)
              results.push(str2)
            } else {
              results.push(str + "<br>")
            }
          }
        }
        console.log(results);
        this.gjzhys1 = results.join(",")
        console.log(this.gjzhys1)
      }
    },
    closeShow() {
      this.showYun = false;
      this.showNJD = false;
      this.showFeng = false;
      this.showJCYD = false;
      this.showQW = false;
      this.showFJJB = false;
      this.showJYY = false;
      this.showCDB = false;
      this.showDB = false;
      this.showTCJL = false;
      this.showDQSJ = false;
      this.showHZB = false;
      this.showSSPM = false;
      this.showHK = false;
      this.showHL = false;
      this.showNB = false;
      this.showHYF = false;
      this.showZCDW = false;
      this.showKZXLD = false;
      this.showXQXSD = false;
      this.showSSD = false;
      this.showGZD = false;
      this.showZSJTF = false;
      this.showDDDD = false;
      this.showDDMZD = false;
    },
    onEditorBlur(quill) {
      console.log('editor blur!', quill);
    },
    onEditorFocus(quill) {
      console.log('editor focus!', quill);
    },
    onEditorReady(quill) {
      console.log('editor ready!', quill);
    },
    handleImageAdded(file, Editor, cursorLocation, resetUploader) {
      const formData = new FormData();
      formData.append('image', file);

      fetch('https://your-backend-api.com/upload', {
        method: 'POST',
        body: formData
      })
        .then(response => response.json())
        .then(data => {
          const imageUrl = data.url; // 假设后端返回图片的 URL
          Editor.insertEmbed(cursorLocation, 'image', imageUrl);
          resetUploader();
        })
        .catch((error) => {
          console.error('Error:', error);
        });
    },
    getGzList(type) {
      this.closeShow();
      var data = {
        type: type
      }
      getGz(data).then((res) => {
        this.gzlist = res.list;
        if (type == "起降") {
          var yun = res.list.filter(l => l.infoType === "云");
          // 初始化 yunlist 数组
          this.yunlist = [];
          yun.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            yun.text = "";
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    yun.text += content;
                  }
                })
                yun.text += `<br>`;
              }
            })
            this.yunlist.push({
              text: yun.text,
              type: '起降',
              option: '操作'
            });
          });
          this.showYun = true;


          var njd = res.list.filter(l => l.infoType === "能见度");
          this.njdlist = [];
          njd.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            njd.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    njd.text += content;
                  }
                })
                njd.text += `<br>`;
              }
            })
            this.njdlist.push({
              text: njd.text,
              type: '起降',
              option: '操作'
            });
          });
          this.showNJD = true;

          var feng = res.list.filter(l => l.infoType === "风");
          this.fenglist = [];
          feng.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            feng.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    feng.text += content;
                  }
                })
                feng.text += `<br>`;
              }
            })
            this.fenglist.push({
              text: feng.text,
              type: '起降',
              option: '操作'
            });
          });
          this.showFeng = true;

          var jcyd = res.list.filter(l => l.infoType === "舰船摇荡");
          this.jcydlist = [];
          jcyd.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            jcyd.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    jcyd.text += content;
                  }
                })
                jcyd.text += `<br>`;
              }
            })
            this.jcydlist.push({
              text: jcyd.text,
              type: '起降',
              option: '操作'
            });
          });
          this.showJCYD = true;
        }
        if (type == "飞行") {
          var qw = res.list.filter(l => l.infoType === "气温");
          this.qwlist = [];
          qw.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            qw.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    qw.text += content;
                  }
                })
                qw.text += `<br>`;
              }
            })
            this.qwlist.push({
              text: qw.text,
              type: '飞行',
              option: '操作'
            });
          });
          this.showQW = true;

          var feng1 = res.list.filter(l => l.infoType === "风");
          this.fenglist = [];
          feng1.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            feng1.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    feng1.text += content;
                  }
                })
                feng1.text += `<br>`;
              }
            })
            this.fenglist.push({
              text: feng1.text,
              type: '飞行',
              option: '操作'
            });
          });
          this.showFeng = true;

          var fjjb = res.list.filter(l => l.infoType === "飞机积冰");
          this.fjjblist = [];
          fjjb.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            fjjb.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    fjjb.text += content;
                  }
                })
                fjjb.text += `<br>`;
              }
            })
            this.fjjblist.push({
              text: fjjb.text,
              type: '飞行',
              option: '操作'
            });
          });
          this.showFJJB = true;

          var jyy = res.list.filter(l => l.infoType === "积雨云");
          this.jyylist = [];
          jyy.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            jyy.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    jyy.text += content;
                  }
                })
                jyy.text += `<br>`;
              }
            })
            this.jyylist.push({
              text: jyy.text,
              type: '飞行',
              option: '操作'
            });
          });
          this.showJYY = true;
        }
        if (type == "通信") {
          var cdb = res.list.filter(l => l.infoType === "超短波");
          this.cdblist = [];
          cdb.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            cdb.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    cdb.text += content;
                  }
                })
                cdb.text += `<br>`;
              }
            })
            this.cdblist.push({
              text: cdb.text,
              type: '通信',
              option: '操作'
            });
          });
          this.showCDB = true;

          var db = res.list.filter(l => l.infoType === "短波");
          this.dblist = [];
          db.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            db.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    db.text += content;
                  }
                })
                db.text += `<br>`;
              }
            })
            this.dblist.push({
              text: db.text,
              type: '通信',
              option: '操作'
            });
          });
          this.showDB = true;
        }
        if (type == "探测") {
          var tcjl = res.list.filter(l => l.infoType1 === "探测距离");
          this.tcjllist = [];
          tcjl.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            tcjl.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    tcjl.text += content;
                  }
                })
                tcjl.text += `<br>`;
              }
            })
            this.tcjllist.push({
              text: tcjl.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showTCJL = true;

          var dqsj = res.list.filter(l => l.infoType1 === "大气衰减");
          this.dqsjlist = [];
          dqsj.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            dqsj.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    dqsj.text += content;
                  }
                })
                dqsj.text += `<br>`;
              }
            })
            this.dqsjlist.push({
              text: dqsj.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showDQSJ = true;

          var hzb = res.list.filter(l => l.infoType1 === "海杂波");
          this.hzblist = [];
          hzb.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            hzb.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    hzb.text += content;
                  }
                })
                hzb.text += `<br>`;
              }
            })
            this.hzblist.push({
              text: hzb.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showHZB = true;

          var sspm = res.list.filter(l => l.infoType1 === "声速剖面");
          this.sspmlist = [];
          sspm.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            sspm.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    sspm.text += content;
                  }
                })
                sspm.text += `<br>`;
              }
            })
            this.sspmlist.push({
              text: sspm.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showSSPM = true;

          var hk = res.list.filter(l => l.infoType1 === "海况");
          this.hklist = [];
          hk.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            hk.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    hk.text += content;
                  }
                })
                hk.text += `<br>`;
              }
            })
            this.hklist.push({
              text: hk.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showHK = true;

          var hl = res.list.filter(l => l.infoType1 === "海流");
          this.hllist = [];
          hl.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            hl.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    hl.text += content;
                  }
                })
                hl.text += `<br>`;
              }
            })
            this.hllist.push({
              text: hl.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showHL = true;

          var nb = res.list.filter(l => l.infoType1 === "内波");
          this.nblist = [];
          nb.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            hl.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    nb.text += content;
                  }
                })
                nb.text += `<br>`;
              }
            })
            this.nblist.push({
              text: nb.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showNB = true;

          var hyf = res.list.filter(l => l.infoType1 === "海洋锋");
          this.hyflist = [];
          hyf.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            hl.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    hyf.text += content;
                  }
                })
                hyf.text += `<br>`;
              }
            })
            this.hyflist.push({
              text: hyf.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showHYF = true;

          var zcdw = res.list.filter(l => l.infoType1 === "中尺度涡");
          this.zcdwlist = [];
          zcdw.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            hl.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    zcdw.text += content;
                  }
                })
                zcdw.text += `<br>`;
              }
            })
            this.zcdwlist.push({
              text: zcdw.text,
              type: '探测',
              option: '操作'
            });
          });
          this.showZCDW = true;
        }
        if (type == "攻击") {
          var kzxld = res.list.filter(l => l.infoType1 === "空中下落段");
          this.kzxldlist = [];
          kzxld.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            kzxld.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    kzxld.text += content;
                  }
                })
                kzxld.text += `<br>`;
              }
            })
            this.kzxldlist.push({
              text: kzxld.text,
              type: '攻击',
              option: '操作'
            });
          });
          this.showKZXLD = true;

          var xqxsd = res.list.filter(l => l.infoType1 === "下潜寻深段");
          this.xqxsdlist = [];
          xqxsd.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            xqxsd.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    xqxsd.text += content;
                  }
                })
                xqxsd.text += `<br>`;
              }
            })
            this.xqxsdlist.push({
              text: xqxsd.text,
              type: '攻击',
              option: '操作'
            });
          });
          this.showXQXSD = true;

          var ssd = res.list.filter(l => l.infoType1 === "搜索段");
          this.ssdlist = [];
          ssd.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            ssd.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    ssd.text += content;
                  }
                })
                ssd.text += `<br>`;
              }
            })
            this.ssdlist.push({
              text: ssd.text,
              type: '攻击',
              option: '操作'
            });
            console.log(this.ssdlist)
          });
          this.showSSD = true;

          var gzd = res.list.filter(l => l.infoType1 === "跟踪段");
          this.gzdlist = [];
          gzd.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            gzd.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    gzd.text += content;
                  }
                })
                gzd.text += `<br>`;
              }
            })
            this.gzdlist.push({
              text: gzd.text,
              type: '攻击',
              option: '操作'
            });
          });
          this.showGZD = true;

          var zsjtf = res.list.filter(l => l.infoType1 === "直升机突防");
          this.zsjtflist = [];
          zsjtf.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            zsjtf.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    zsjtf.text += content;
                  }
                })
                zsjtf.text += `<br>`;
              }
            })
            this.zsjtflist.push({
              text: zsjtf.text,
              type: '攻击',
              option: '操作'
            });
          });
          this.showZSJTF = true;

          var dddd = res.list.filter(l => l.infoType1 === "导弹弹道");
          this.ddddlist = [];
          dddd.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            dddd.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    dddd.text += content;
                  }
                })
                dddd.text += `<br>`;
              }
            })
            this.ddddlist.push({
              text: dddd.text,
              type: '攻击',
              option: '操作'
            });
          });
          this.showDDDD = true;

          var ddmzd = res.list.filter(l => l.infoType1 === "导弹末制导");
          this.ddmzdlist = [];
          ddmzd.forEach(item => {
            const text = item.text;
            let content = '';
            var yuanSu = text.replace(/^"|"$/g, '').split("<br>");
            ddmzd.text = '';
            yuanSu.forEach(y => {
              if (y !== "" && y !== undefined) {
                var pS = y.split(",");
                pS.forEach(p => {
                  if (p !== "" && p !== undefined) {
                    console.log(p)
                    //检查文本是否以 .png 结尾
                    if (p.endsWith(".png")) {
                      // 如果是图片地址
                      content = `<img src="${p}" alt="" style="width: 40%; height: auto; object-fit: contain;">`;
                    } else if (p === "<br>") {
                      content = `<br>`;
                    } else {
                      // 如果是普通文本
                      content = p;// style="color:#fff"
                    }
                    ddmzd.text += content;
                  }
                })
                ddmzd.text += `<br>`;
              }
            })
            this.ddmzdlist.push({
              text: ddmzd.text,
              type: '攻击',
              option: '操作'
            });
          });
          this.showDDMZD = true;
        }
        this.showList = true

        this.jslist = [];
        if (type == "起降") {
          this.isQjjs = true;
          this.isFxjs = false;
          this.isTxjs = false;
          this.isTcjs = false;
          this.isGjjs = false;
        }
        if (type == "飞行") {
          this.isQjjs = false;
          this.isFxjs = true;
          this.isTxjs = false;
          this.isTcjs = false;
          this.isGjjs = false;
        }
        if (type == "探测") {
          this.isQjjs = false;
          this.isFxjs = false;
          this.isTxjs = false;
          this.isTcjs = true;
          this.isGjjs = false;
        }
        if (type == "通信") {
          this.isQjjs = false;
          this.isFxjs = false;
          this.isTxjs = true;
          this.isTcjs = false;
          this.isGjjs = false;
        }
        if (type == "攻击") {
          this.isQjjs = false;
          this.isFxjs = false;
          this.isTxjs = false;
          this.isTcjs = false;
          this.isGjjs = true;
        }

        // sidebarItems: [


        //   "舰载自卫作战距离",
        //   "击水概率计算",
        //   "自卫作战距离计算",

        // ],
      })
    },
    // 切换侧边栏显示状态
    toggleSidebar() {
      this.sidebarVisible = !this.sidebarVisible;
      this.showList = !this.showList;
    },
    searchTuPu() {
      if (this.rwmc.text != "请选择任务" && this.rwmc.text != undefined) {
        this.form1.type = this.rwmc.text;
      } else {
        this.form1.type = ""
      }
      this.form1.plane = [];
      this.form1.info.info1 = [];
      this.form1.info.info2 = [];
      if (this.fjxh.text != "请选择机型" && this.fjxh.text != undefined) {
        this.form1.plane.push(this.fjxh.text);
      }
      if (this.txzh.text != "请选择通信载荷" && this.txzh.text != undefined) {
        this.form1.info.info1.push(this.txzh.text);
      }
      if (this.tczh.text != "请选择探测载荷" && this.tczh.text != undefined) {
        this.form1.info.info1.push(this.tczh.text);
      }
      if (this.gjzh.text != "请选择攻击载荷" && this.gjzh.text != undefined) {
        this.form1.info.info2.push(this.gjzh.text);
      }
      console.log("还没执行")
      getDomainGraphNew1(this.form1).then((res) => {
        console.log("执行了")
        this.gjjslist = [];
        this.qjjslist = [];
        this.fxjslist = [];
        this.txjslist = [];
        this.tcjslist = [];
        let nodes = res.data.nodes;
        console.log(nodes)
        const DDZZSYFZJCNode = nodes.filter(n => n.jsInfo === "DDZZSYFZJC");
        if (DDZZSYFZJCNode.length > 0) {
          for (let i = 0; i < DDZZSYFZJCNode.length; i++) {
            let name = DDZZSYFZJCNode[i].name;
            this.gjjslist.push({ name: name })
          }
        }
        const LDWLTNode = nodes.filter(n => n.jsInfo === "LDWLT");
        if (LDWLTNode.length > 0) {
          for (let i = 0; i < LDWLTNode.length; i++) {
            let name = LDWLTNode[i].name;
            this.tcjslist.push({ name: name })
          }
        }
        const QJNode = nodes.filter(n => n.jsInfo === "QJFXT");
        if (QJNode.length > 0) {
          for (let i = 0; i < QJNode.length; i++) {
            let name = QJNode[i].name;
            this.qjjslist.push({ name: name })
          }
        }
        const JSGLNode = nodes.filter(n => n.jsInfo === "JSGL");
        if (JSGLNode.length > 0) {
          for (let i = 0; i < JSGLNode.length; i++) {
            let name = JSGLNode[i].name;
            this.gjjslist.push({ name: name })
          }
        }
        const DBDLCNode = nodes.filter(n => n.jsInfo === "DBDLC");
        console.log(DBDLCNode)
        if (DBDLCNode.length > 0) {
          for (let i = 0; i < DBDLCNode.length; i++) {
            let name = DBDLCNode[i].name;
            this.txjslist.push({ name: name })
          }
        }
        const SNJSNode = nodes.filter(n => n.jsInfo === "SNJS");
        if (SNJSNode.length > 0) {
          for (let i = 0; i < SNJSNode.length; i++) {
            let name = SNJSNode[i].name;
            this.tcjslist.push({ name: name })
          }
        }
        const CDBTXNode = nodes.filter(n => n.jsInfo === "CDBTX");
        if (CDBTXNode.length > 0) {
          for (let i = 0; i < CDBTXNode.length; i++) {
            let name = CDBTXNode[i].name;
            this.txjslist.push({ name: name })
          }
        }
        const YLDQGJNode = nodes.filter(n => n.jsInfo === "YLDQGJ");
        if (YLDQGJNode.length > 0) {
          for (let i = 0; i < YLDQGJNode.length; i++) {
            let name = YLDQGJNode[i].name;
            this.gjjslist.push({ name: name })
          }
        }
        const SNJSNode1 = nodes.filter(n => n.jsInfo === "SN1");
        if (SNJSNode1.length > 0) {
          for (let i = 0; i < SNJSNode1.length; i++) {
            let name = SNJSNode1[i].name;
            this.tcjslist.push({ name: name })
          }
        }
      })
    },
    // 选择侧边栏项目
    selectSidebarItem(index) {


      this.selectedSidebarItem = index;
      // 这里可以添加选择项目后的操作，比如加载相关内容
      console.log('选择了:', this.sidebarItems[index]);
      this.getGzList(this.sidebarItems[index]);

    },

    showTime() {
      console.log(this.rwsj)
    },
    //获取计算列表
    getAllJs() {
      var data = {
        "uid": localStorage.getItem("uid"),
        "keyName": this.jsKey
      }
      console.log(data)
      getAllJsResult(data).then((res) => {
        if (res.data) {
          this.tableDataListJs = res.data;
          // if(res.data.useZjsb){
          //   this.tableDataListJs[0].useZjsb = "是";
          // }else {
          //   this.tableDataListJs[0].useZjsb = "否";
          // }
          // let urls = this.tableDataListJs[0].allImg;
          // this.$axios({
          //   // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
          //   url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
          //   method: "get",//get请求方式
          //   params: { urls: urls },
          //   headers: {
          //     'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
          //     'Access-Control-Request-Method': 'GET',
          //     'Access-Control-Request-Headers': 'content-type',
          //   },
          // }).then((res) => {
          //   console.log(res)
          //   this.tableDataListJs[0].allImg = res.data.results[0].url;
          // })
        }
      })
    },
    useInfo(row) {
      //起降风限图
      if (this.jsKey == "QJFXT") {
        const headers = this.$refs.myTable.columns.map(column => ({
          prop: column.property,
          label: column.label
        }));
        if (row.tz == null) {
          row.tz = ""
        }
        this.qjysImg = row.allImg.split(",")[0];
        console.log(row.allImg)

        // 构建结果对象
        const result = {
          headers: headers,
          rowData: row,
          // 也可以构建键值对应的形式
          mappedData: this.mapRowToHeaders(row, headers)
        };


        console.log('生成的JSON:', result);
        const targetKeys = ["舰艇型号", "飞机型号", "航向", "航速", "横摇角度", "纵摇角度", "纵摇周期", "波长", "是否使用助降设备", "助降设备", "调整后航向", "调整后航速", "谐振航速", "能否调整", "原因"];
        const filteredData = {};

        // 遍历并提取
        targetKeys.forEach(key => {
          if (key in result.mappedData) {
            filteredData[key] = result.mappedData[key];
            delete result.mappedData[key]; // 从原数据删除
          }
        });

        /* eslint-disable no-unused-vars */
        const result111 = Object.entries(result.mappedData)
          .filter(([key, value]) => value !== undefined && value !== '' && key !== '图片') // ✅ 正确过滤 value
          .map(([key, value]) => {
            if (value === false) return `${key}：否`;    // false → "否"
            if (value === true) return `${key}：是`;     // true → "是"
            return `${key}：${value}`;                  // 其他情况直接拼接
          })
          .join(", ");
        console.log(result111)
        const result222 = Object.entries(filteredData)
          .filter(([key, value]) => value !== undefined && value !== '') // ✅ 正确过滤 value
          .map(([key, value]) => {
            if (value === false) return `${key}：否`;    // false → "否"
            if (value === true) return `${key}：是`;     // true → "是"
            return `${key}：${value}`;                  // 其他情况直接拼接
          })
          .join(", ");
        console.log(result222); // 输出: "啊啊啊：5000, 水水水水水：3000"
        console.log(this.zzhjys)
        if (this.zzhjys == "<p>请输入起降环境因素</p>") {
          this.zzhjys = "<p>" + result111 + "</p>";
          this.zzhjys += "<p>" + result222 + "</p>";
        } else {
          this.zzhjys += "<p>" + result111 + "</p>";
          this.zzhjys += "<p>" + result222 + "</p>";
        }
        if (this.zzhjys1 == "<p>请输入起降环境因素</p>") {
          this.zzhjys1 = result111;
        } else {
          this.zzhjys1 += result111;
        }
        // this.jzhjys = result222;
        this.dialogVisibleJs = false;
      }
      //短波电离层
      if (this.jsKey == "DBDLC") {
        const headers = this.$refs.myTableTx1.columns.map(column => ({
          prop: column.property,
          label: column.label
        }));
        // 构建结果对象
        const result = {
          headers: headers,
          rowData: row,
          // 也可以构建键值对应的形式
          mappedData: this.mapRowToHeaders(row, headers)
        };
        const result111 = Object.entries(result.mappedData)
          .filter(([key, value]) => value !== undefined && value !== '') // ✅ 正确过滤 value
          .map(([key, value]) => {
            if (value === false) return `${key}：否`;    // false → "否"
            if (value === true) return `${key}：是`;     // true → "是"
            return `${key}：${value}`;                  // 其他情况直接拼接
          });
        // .join(", ");
        console.log(result111[8])
        this.txzhysImg = result111[8].split("图片：")[1];
        delete result111[8];
        if (this.txzhys == "<p>请输入环境对通信载荷的影响</p>") {
          this.txzhys = "<p>" + JSON.stringify(result111) + "</p>";
        } else {
          this.txzhys += "<p>" + JSON.stringify(result111) + "</p>";
        }
        if (this.txzhys1 == "<p>请输入环境对通信载荷的影响</p>") {
          this.txzhys1 = JSON.stringify(result111);
        } else {
          this.txzhys1 += JSON.stringify(result111);
        }
        this.dialogVisibleJs = false;
      }

      if (this.jsKey == "CDBTX") {
        const headers = this.$refs.myTableTx1.columns.map(column => ({
          prop: column.property,
          label: column.label
        }));
        // 构建结果对象
        const result = {
          headers: headers,
          rowData: row,
          // 也可以构建键值对应的形式
          mappedData: this.mapRowToHeaders(row, headers)
        };
        const result111 = Object.entries(result.mappedData)
          .filter(([key, value]) => value !== undefined && value !== '') // ✅ 正确过滤 value
          .map(([key, value]) => {
            if (value === false) return `${key}：否`;    // false → "否"
            if (value === true) return `${key}：是`;     // true → "是"
            return `${key}：${value}`;                  // 其他情况直接拼接
          });
        // .join(", ");
        if (this.txzhys == "<p>请输入环境对通信载荷的影响</p>") {
          this.txzhys = "<p>" + JSON.stringify(result111) + "</p>";
          console.log(this.txzhys)
        } else {
          this.txzhys += "<p>" + JSON.stringify(result111) + "</p>";
          console.log(this.txzhys)
        }
        if (this.txzhys1 == "<p>请输入环境对通信载荷的影响</p>") {
          this.txzhys1 = JSON.stringify(result111);
        } else {
          this.txzhys1 += JSON.stringify(result111);
        }
        this.dialogVisibleJs = false;
      }

      //大气降水
      if (this.jsKey == "DQJS") {
        this.tczhysImg = row.allImg;
        this.dialogVisibleJs = false;
      }
      if (this.jsKey == "JSGL") {
        this.gjzhysImg = row.allImg;
        this.dialogVisibleJs = false;
      }
      if (this.jsKey == "SNJS") {
        console.log(row)
        console.log(this.tczhys)
        if (this.tczhys == "<p>请输入环境对探测载荷的影响</p>") {
          this.tczhys = "<p>" + JSON.stringify(row) + "</p>";
        } else {
          this.tczhys += "<p>" + JSON.stringify(row) + "</p>";
        }
        if (this.tczhys1 == "<p>请输入环境对探测载荷的影响</p>") {
          this.tczhys1 = JSON.stringify(row);
        } else {
          this.tczhys1 += JSON.stringify(row);
        }
        this.dialogVisibleJs = false;
      }
      if (this.jsKey == "SN1") {
        console.log(row)
        const textData = { ...row };
        delete textData.allImg; // 移除图片字段
        console.log(this.tczhys)
        console.log(this.tczhys1)
        if (this.tczhys == "<p>请输入环境对探测载荷的影响</p>") {
          this.tczhys = "<p>" + JSON.stringify(textData) + "</p>";
        } else {
          this.tczhys += "<p>" + JSON.stringify(textData) + "</p>";
        }
        if (this.tczhys1 == "<p>请输入环境对探测载荷的影响</p>") {
          this.tczhys1 = JSON.stringify(textData);
        } else {
          this.tczhys1 += JSON.stringify(textData);
        }
        console.log(this.tczhys)
        console.log(this.tczhys1)
        this.tczhysIndex = this.tczhysIndex + 1
        const imgData = row.allImg.split(",");
        this.tczhysImg = imgData[0];
        this.tczhysImg1 = imgData[1];
        this.dialogVisibleJs = false;
      }
      if (this.jsKey == "DDZZSYFZJC") {
        console.log(row)
        const textData = { ...row };
        delete textData.allImg; // 移除图片字段
        console.log(this.gjzhys)
        console.log(this.gjzhys1)
        if (this.gjzhys == "<p>请输入环境对攻击载荷的影响</p>") {
          this.gjzhys = "<p>" + JSON.stringify(textData) + "</p>";
        } else {
          this.gjzhys += "<p>" + JSON.stringify(textData) + "</p>";
        }
        if (this.gjzhys1 == "<p>请输入环境对攻击载荷的影响</p>") {
          this.gjzhys1 = JSON.stringify(textData);
        } else {
          this.gjzhys1 += JSON.stringify(textData);
        }
        console.log(this.tczhys)
        console.log(this.tczhys1)
        const imgData = row.allImg;
        this.gjzhysImg = imgData;
        this.dialogVisibleJs = false;
      }
      if (this.jsKey == "YLDQGJ") {
        console.log(row)
        const textData = { ...row };
        delete textData.allImg; // 移除图片字段
        console.log(this.gjzhys)
        console.log(this.gjzhys1)
        if (this.gjzhys == "<p>请输入环境对攻击载荷的影响</p>") {
          this.gjzhys = "<p>" + JSON.stringify(textData) + "</p>";
        } else {
          this.gjzhys += "<p>" + JSON.stringify(textData) + "</p>";
        }
        if (this.gjzhys1 == "<p>请输入环境对攻击载荷的影响</p>") {
          this.gjzhys1 = JSON.stringify(textData);
        } else {
          this.gjzhys1 += JSON.stringify(textData);
        }
        console.log(this.tczhys)
        console.log(this.tczhys1)
        const imgData = row.allImg;
        this.gjzhysImg = imgData;
        this.dialogVisibleJs = false;
      }
      if (this.jsKey == "LDWLT") {
        console.log(row)
        const textData = { ...row };
        delete textData.allImg; // 移除图片字段
        console.log(this.tczhys)
        console.log(this.tczhys1)
        if (this.tczhys == "<p>请输入环境对探测载荷的影响</p>") {
          this.tczhys = "<p>" + JSON.stringify(textData) + "</p>";
        } else {
          this.tczhys += "<p>" + JSON.stringify(textData) + "</p>";
        }
        if (this.tczhys1 == "<p>请输入环境对探测载荷的影响</p>") {
          this.tczhys1 = JSON.stringify(textData);
        } else {
          this.tczhys1 += JSON.stringify(textData);
        }
        console.log(this.tczhys)
        console.log(this.tczhys1)
        this.tczhysIndex = this.tczhysIndex + 1
        const imgData = row.allImg.split(",");
        this.tczhysImg = imgData[0];
        this.tczhysImg1 = imgData[1];
        this.dialogVisibleJs = false;
      }
    },
    mapRowToHeaders(row, headers) {
      const mapped = {};
      headers.forEach(header => {
        if (header.prop) {
          mapped[header.label] = row[header.prop];
        }
      });
      return mapped;
    },

    changeJsType(type) {
      this.jsKey = type

      this.getAllJs()
    },
    historyJsTest() {
      this.dialogVisibleJs = true;
      this.tableDataListJs = [];
      this.jsKey = "";
      this.jsType = undefined
      this.changeJsType("QJFXT")

    },
    historyJs(row) {
      this.dialogVisibleJs = true;
      this.tableDataListJs = [];
      this.jsKey = "";
      this.jsType = undefined
      if (row.name == "XXXX辅助决策") {
        this.changeJsType("QJFXT");
      }
      if (row.name == "电离层对短波通信的影响分析软件") {
        this.changeJsType("DBDLC")
      }
      if (row.name == "声呐探测距离估算软件") {
        this.changeJsType("SNJS")
      }
      if (row.name == "海洋环境对声呐探测的影响分析软件") {
        this.changeJsType("SN1")
      }
      if (row.name == "大气波导对电磁场传播的影响分析软件") {
        this.changeJsType("LDWLT")
      }
      if (row.name == "大气环境对雷达探测的影响分析软件") {
        this.changeJsType("DQJS")
      }
      if (row.name == "舰载直升机空舰导弹作战使用辅助决策软件") {
        this.changeJsType("DDZZSYFZJC")
      }
      if (row.name == "舰载直升机航空鱼雷作战使用辅助决策软件") {
        this.changeJsType("YLDQGJ")
      }
      if (row.name == "面向舰机超短波通信的表面波导可用性评估软件 ") {
        this.changeJsType("CDBTX")
      }
    },

    openJs(type) {
      this.dialogVisibleJs = true;
      this.tableDataListJs = [];
      this.jsKey = "";
      this.jsType = undefined
      if (type == 0) {
        this.jsType = 0
        this.changeJsType("QJFXT");
      }
      if (type == 1) {
        this.jsType = 1
        this.buttonList = [
          { text: "超短波", type: "CDB" },
          { text: "短波", type: "DBDLC" }
        ]
      }
      if (type == 2) {
        this.jsType = 2
        this.buttonList = [
          { text: "水声传播规律", type: "Bellhop" },
          { text: "声呐距离计算", type: "SNJS" },
          { text: "雷达威力图", type: "LDWLT" },
          { text: "雷达探测受天气影响", type: "DQJS" },
        ]
      }
      if (type == 3) {
        this.jsType = 3
        this.buttonList = [
          { text: "鱼雷自导作用距离", type: "YLZDZY" },
          { text: "空舰导弹击水概率", type: "JSGL" },
          { text: "空舰导弹自导作用距离", type: "ZDZYJL" },
        ]
      }
    },


    sumbitConlumInfo() {
      if (this.comlunId == undefined) {
        let data = {
          "columName": this.comlunName,
          "columkey": this.comlunkey

        }
        insertTable(data).then((res) => {
          console.log(res);
          this.showEdit = false;
          this.getAllTable();
        })
      } else {
        let data = {
          "columName": this.comlunName,
          "columkey": this.comlunkey

        }
        editTable(data).then((res) => {
          console.log(res);
          this.showEdit = false;
          this.getAllTable();
        })
      }
    },
    editLieBiao(row) {
      this.comlunId = row.id;
      this.showEdit = true;
    },
    addLieBiao() {
      this.showEdit = true;
    },
    getAllTable() {
      var data = {};
      getTableList(data).then((res) => {
        console.log(res.list);
        this.showLieBiao = true;
        this.lieBiaoList = res.list
      })
    },
    baoCun() {

      this.dialogVisibleInput = true;
    },
    // lookInfo(row) {
    //   console.log(row.bgjilu)
    //   this.bgId = row.id;
    //   this.baoGaoName = row.bgName
    //   let jsonObj = {};
    //   jsonObj = JSON.parse(row.bgjilu);


    //   this.rwmc = jsonObj.textData.taskName;
    //   this.rwmd = jsonObj.textData.taskTarget;
    //   this.rwhq = jsonObj.textData.haiqv;
    //   this.zzhjys = jsonObj.textData.zzhjys;
    //   this.jzhjys = jsonObj.textData.jzhjys;
    //   this.fxhjys = jsonObj.textData.fxhjys;
    //   this.txzhys = jsonObj.textData.txzhys;
    //   this.tczhys = jsonObj.textData.tczhys;
    //   this.tczhysImg = jsonObj.textData.tczhysImg;
    //   this.gjzhys = jsonObj.textData.gjzhys;


    //   this.dynamicColumns = jsonObj.tableData[0].users
    //   this.rwhj = [];
    //   var hj = {};
    //   for (let a = 0; a < this.dynamicColumns.length; a++) {
    //     let key = this.dynamicColumns[a].prop
    //     hj[key] = jsonObj.tableData[0].rows[0][a];
    //   }
    //   this.rwhj.push(hj)

    //   this.jtbl = [];
    //   for (let v = 0; v < jsonObj.tableData[1].rows.length; v++) {
    //     let jtdata = {
    //       xvhao: jsonObj.tableData[1].rows[v][0],
    //       lx: jsonObj.tableData[1].rows[v][1],
    //       xinghao: jsonObj.tableData[1].rows[v][2],
    //       xjh: jsonObj.tableData[1].rows[v][3],
    //       ms: jsonObj.tableData[1].rows[v][4],
    //       bz: jsonObj.tableData[1].rows[v][5],
    //     }
    //     this.jtbl.push(jtdata)
    //   }


    //   this.zsjbl = [];
    //   for (let v = 0; v < jsonObj.tableData[2].rows.length; v++) {
    //     let jtdata1 = {
    //       xvhao: jsonObj.tableData[2].rows[v][0],
    //       lx: jsonObj.tableData[2].rows[v][1],
    //       xh: jsonObj.tableData[2].rows[v][2],
    //       xjh: jsonObj.tableData[2].rows[v][3],
    //       ms: jsonObj.tableData[2].rows[v][4],
    //       bz: jsonObj.tableData[2].rows[v][5],
    //     }
    //     this.zsjbl.push(jtdata1)
    //   }


    //   this.txzh = [];
    //   for (let v = 0; v < jsonObj.tableData[3].rows.length; v++) {
    //     let jtdata1 = {
    //       txfs: jsonObj.tableData[3].rows[v][0],
    //       txzb: jsonObj.tableData[3].rows[v][1],
    //       bz: jsonObj.tableData[3].rows[v][2],
    //     }
    //     this.txzh.push(jtdata1)
    //   }


    //   this.tczh = [];
    //   for (let v = 0; v < jsonObj.tableData[4].rows.length; v++) {
    //     let jtdata1 = {
    //       tcsb: jsonObj.tableData[4].rows[v][0],
    //       tczb: jsonObj.tableData[4].rows[v][1],
    //       bz: jsonObj.tableData[4].rows[v][2],
    //     }
    //     this.tczh.push(jtdata1)
    //   }


    //   this.gjzh = [];
    //   for (let v = 0; v < jsonObj.tableData[5].rows.length; v++) {
    //     let jtdata1 = {
    //       wqlx: jsonObj.tableData[5].rows[v][0],
    //       wqzb: jsonObj.tableData[5].rows[v][1],
    //       bz: jsonObj.tableData[5].rows[v][2],
    //     }
    //     this.gjzh.push(jtdata1)
    //   }


    //   this.indexNum = this.indexNum + 1
    //   this.dialogVisibleList = false;
    // },
    downLoadWord(row) {
      // 创建下载链接
      const url = row.bgUrl;
      const link = document.createElement('a');
      link.href = url;
      link.setAttribute('download', row.bgName + '.docx');
      document.body.appendChild(link);
      link.click();

      // 清理
      document.body.removeChild(link);
      window.URL.revokeObjectURL(url);

    },
    getAllJl() {
      var data = {};
      getAllHistory(data).then((res) => {
        this.dialogVisibleList = true;
        this.tableDataList = [];
        console.log(res)
        this.tableDataList = res.list;
        console.log(this.tableDataList)


      })
    },
    loadPng() {
      var aa = this.visGraph.saveImage();
      this.handleCapture(aa)
      this.showTp1 = false

      setTimeout(() => {
        this.qjtp = this.ImgG;
      }, 1000)


    },
    loadPng1() {
      var aa = this.visGraph1.saveImage();
      this.handleCapture(aa)
      this.showTp2 = false
      setTimeout(() => {
        this.fxtp = this.ImgG;
      }, 100)

    },
    loadPng2() {
      var aa = this.visGraph2.saveImage();
      this.handleCapture(aa)
      this.showTp3 = false
      setTimeout(() => {
        this.txtp = this.ImgG;
      }, 100)

    },
    loadPng3() {
      var aa = this.visGraph3.saveImage();
      this.handleCapture(aa)
      this.showTp4 = false
      setTimeout(() => {
        this.tctp = this.ImgG;
      }, 100)

    },
    loadPng4() {
      var aa = this.visGraph4.saveImage();
      this.handleCapture(aa)
      this.showTp5 = false
      setTimeout(() => {
        this.gjtp = this.ImgG;
      }, 100)

    },
    addGz() {
      this.showGz = true;
    },
    submitGz() {
      var params = {
        text: "",
        type: "",
        infoType: "",
        infoType1: "",
      }
      const tempDiv = document.createElement('div');
      tempDiv.innerHTML = this.gzwenben;
      // 用于存储结果
      let result = "";

      // 遍历所有子节点
      const nodes = Array.from(tempDiv.childNodes);
      nodes.forEach(node => {
        if (node.innerHTML.includes("<img")) {
          // 如果是图片节点，提取src属性
          let innerHTML = node.innerHTML;
          console.log(innerHTML);
          const imgRegex = /<img[^>]+>/g;
          const srcRegex = /<img[^>]+src="([^">]+)"/g;
          const contentRegex = />([^<]+)</g;
          let matches = [];
          // let matches1 = [];
          const innerHTML1 = innerHTML;
          const matches1 = Array.from(innerHTML.matchAll(imgRegex));
          for (const match of matches1) {
            console.log(match)
            const ms = Array.from(match[0].matchAll(srcRegex));
            console.log(ms)
            innerHTML = innerHTML.replace(match[0], ",");
            matches.push(ms[0][1]);
          }
          console.log(innerHTML)
          const matches2 = Array.from(innerHTML.matchAll(contentRegex));
          for (const match of matches2) {
            innerHTML = innerHTML.replace(match[1], ",");
            matches.push(match[1]);
          }
          let inputs = innerHTML.split(",")
          for (const input of inputs) {
            if (input !== null && input !== "") {
              matches.push(input)
            }
          }
          matches.sort((a, b) => {
            const aIndex = innerHTML1.indexOf(a);
            const bIndex = innerHTML1.indexOf(b);
            return aIndex - bIndex;
          })
          console.log(matches)
          for (let i = 0; i < matches.length; i++) {
            if (result == "") {
              result = result + matches[i];
            } else if (result.endsWith("<br>")) {
              result = result + matches[i];
            } else {
              result = result + "," + matches[i];
            }
          }
        } else {
          // 如果是文本节点，提取文本内容
          if (result == "") {
            result = result + node.innerHTML;
          } else if (result.endsWith("<br>")) {
            result = result + node.innerHTML;
          } else {
            result = result + "," + node.innerHTML;
          }
        }
        result = result + "," + "<br>";
        console.log(result);
      });
      params.text = JSON.stringify(result);
      params.type = this.gzType;
      params.infoType = this.gzInfoType;
      params.infoType1 = this.gzInfoType1;
      console.log(params);
      insertGz(params);
      this.showGz = false;
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

        this.ImgG = res.data.url

      })


    },

    async exportAllWord() {
      //任务环境
      this.hjys = {};
      this.hjys.tableTitle = "任务环境";
      this.hjys.headers = []
      this.hjys.users = [...this.dynamicColumns, ...this.dynamicColumns1]
      for (let a = 0; a < this.dynamicColumns.length; a++) {
        this.hjys.headers.push(this.dynamicColumns[a].label)
      }
      for (let a = 0; a < this.dynamicColumns1.length; a++) {
        this.hjys.headers.push(this.dynamicColumns1[a].label)
      }
      this.hjys.rows = this.rwhj.map(obj => Object.values(obj));
      this.allExportList.push(this.hjys)
      console.log(this.hjys)


      //舰艇
      // this.jt = {};
      // this.jt.tableTitle = "舰艇兵力";
      // this.jt.headers = ["序号", "类型", "型号", "舷(机)号", "描述", "备注"];
      // this.jt.rows = this.jtbl.map(obj => Object.values(obj));
      // this.allExportList.push(this.jt)


      //直升机
      // this.zsj = {};
      // this.zsj.tableTitle = "舰载直升机兵力";
      // this.zsj.headers = ["序号", "类型", "型号", "舷(机)号", "描述", "备注"];
      // this.zsj.rows = this.zsjbl.map(obj => Object.values(obj));
      // this.allExportList.push(this.zsj)


      //通信载荷
      // this.tx = {};
      // this.tx.tableTitle = "通信载荷";
      // this.tx.headers = ["通信方式", "通信装备", "备注"],
      //   this.tx.rows = this.txzh.map(obj => Object.values(obj));
      // this.allExportList.push(this.tx)


      //探测载荷
      // this.tc = {};
      // this.tc.tableTitle = "探测载荷";
      // this.tc.headers = ["探测设备", "探测装备", "备注"],
      //   this.tc.rows = this.tczh.map(obj => Object.values(obj));
      // this.allExportList.push(this.tc)


      //攻击载荷
      // this.gj = {};
      // this.gj.tableTitle = "攻击载荷";
      // this.gj.headers = ["武器类型", "武器装备", "备注"],
      //   this.gj.rows = this.gjzh.map(obj => Object.values(obj));
      // this.allExportList.push(this.gj)


      var task = {
        "taskName": this.rwmc.text,
        "taskTarget": this.rwmd,
        "taskTime": this.rwsj,
        "jtxh": this.jtxh.text,
        "fjxh": this.fjxh.text,
        "haiqv": this.rwhq,
        "qjtp": this.qjtp,
        "zzhjys": this.zzhjys1,
        "jzxdys": this.jzhjys,
        "qjysImg": this.qjysImg,
        "fxtp": this.fxtp,
        "fxhjys": this.fxhjys1,
        "txzh": this.txzh.text,
        "txtp": this.txtp,
        "txzhys": this.txzhys1,
        "txzhysImg": this.txzhysImg,
        "tczh": this.tczh.text,
        "tctp": this.tctp,
        "tczhys": this.tczhys1,
        "tczhysImg": this.tczhysImg,
        "tczhysImg1": this.tczhysImg1,
        "gjzh": this.gjzh.text,
        "gjtp": this.gjtp,
        "gjzhys": this.gjzhys1,
        "gjzhysImg": this.gjzhysImg,


      }
      var data = {
        "tableData": this.allExportList,
        "textData": task
      }
      console.log(data)

      try {
        const response = await axios.post(
          '\n' +
          'http://localhost:10035/api/generate-word-from-template',
          data,
          {
            headers: { 'Authorization': 'Bearer ' + getToken() },
          }
        );

        // console.log(response.data.data.url)


        //保存记录
        var jl = JSON.stringify(data);
        if (this.bgId == undefined) {
          let dataFinal = {
            "bgName": this.baoGaoName,
            "bgjilu": jl,
            "uid": localStorage.getItem("uid"),
            "bgUrl": response.data.data.url
          }
          insertBaoGao(dataFinal).then((res) => {
            console.log(res)
            this.dialogVisibleInput = false;
            this.baoGaoName = ""
            this.getAllJl();
          })
        } else {
          let dataFinal = {
            "id": this.bgId,
            "bgName": this.baoGaoName,
            "bgjilu": jl,
            "uid": localStorage.getItem("uid"),
            "bgUrl": response.data.data.url
          }
          editBaoGao(dataFinal).then((res) => {
            console.log(res)
            this.dialogVisibleInput = false;
            this.bgId = undefined;
            this.baoGaoName = "";
            this.getAllJl();
          })
        }


      } catch (error) {
        console.error('生成Word失败:', error);
        alert('生成Word文档失败，请检查控制台日志');
      }


    },


    async getHistoryNew() {
      this.tableDataList = [];
      this.allExportList = [];

      // 任务环境
      // this.hjys = {};
      // console.log(JSON.parse(JSON.stringify(this.hjys)))
      // this.hjys.tableTitle = "任务环境";
      // this.hjys.headers = []
      // this.hjys.users = [...this.dynamicColumns,...this.dynamicColumns1]
      // for (let a = 0; a < this.dynamicColumns.length; a++) {
      //   this.hjys.headers.push(this.dynamicColumns[a].label)
      // }
      // for (let a = 0; a < this.dynamicColumns1.length; a++) {
      //   this.hjys.headers.push(this.dynamicColumns1[a].label)
      // }
      // console.log(JSON.parse(JSON.stringify(this.hjys)))
      // this.hjys.rows = this.rwhj.map(obj => Object.values(obj));
      // console.log(JSON.parse(JSON.stringify(this.hjys)))
      // this.allExportList.push(this.hjys)
      // console.log(JSON.parse(JSON.stringify(this.allExportList)))


      //舰艇
      // this.jt = {};
      // this.jt.tableTitle = "舰艇兵力";
      // this.jt.headers = ["序号", "类型", "型号", "舷(机)号", "描述", "备注"];
      // this.jt.rows = this.jtbl.map(obj => Object.values(obj));
      // this.allExportList.push(this.jt)


      //直升机
      // this.zsj = {};
      // this.zsj.tableTitle = "舰载直升机兵力";
      // this.zsj.headers = ["序号", "类型", "型号", "舷(机)号", "描述", "备注"];
      // this.zsj.rows = this.zsjbl.map(obj => Object.values(obj));
      // this.allExportList.push(this.zsj)


      //通信载荷
      // this.tx = {};
      // this.tx.tableTitle = "通信载荷";
      // this.tx.headers = ["通信方式", "通信装备", "备注"],
      // this.tx.rows = this.txzh.map(obj => Object.values(obj));
      // this.allExportList.push(this.tx)


      //探测载荷
      // this.tc = {};
      // this.tc.tableTitle = "探测载荷";
      // this.tc.headers = ["探测设备", "探测装备", "备注"],
      // this.tc.rows = this.tczh.map(obj => Object.values(obj));
      // this.allExportList.push(this.tc)


      //攻击载荷
      // this.gj = {};
      // this.gj.tableTitle = "攻击载荷";
      // this.gj.headers = ["武器类型", "武器装备", "备注"],
      // this.gj.rows = this.gjzh.map(obj => Object.values(obj));
      // this.allExportList.push(this.gj)


      // console.log(this.allExportList)
      // var task = {
      //   "taskName": this.rwmc,
      //   "taskTarget": this.rwmd,
      //   "taskTime": this.rwsj,
      //   "haiqv": this.rwhq,
      // }
      var task = {
        "task": this.task,
        "ship": this.ship,
        "plane": this.plane,
        "dqtx": this.dqtx,
        "dqtc": this.dqtc,
        "dqgj": this.dqgj,
        "dqfx": this.dqfx,
        "dqfs": this.dqfs,
        "dqydg": this.dqydg,
        "dqnjd": this.dqnjd,
        "dqdqwd": this.dqdqwd,
        "dqjsl": this.dqjsl,
        "dqdqbd": this.dqdqbd,
        "dqhk": this.dqhk,
        "dqlx": this.dqlx,
        "dqls": this.dqls,
        "dqhs": this.dqhs
      }
      console.log()
      var data = {
        // "tableData": this.allExportList,
        "textData": task
      }
      var jl = JSON.stringify(data);
      var dataNew = {
        "bgjilu": jl
      }


      getAllHistory(dataNew).then((res) => {
        console.log(res.list);
        this.tableDataList = res.list
      })
    },


    //新增列
    addNewColumn() {
      this.dialogTableVisible = true;
    },
    getTable() {
      getTableComlun().then((res) => {
        this.allTable = res.list

      })
    },

    handleChange(value) {

      const selected = this.allTable.find(item => item.columName === value)
      console.log(selected)
      this.form.propName = selected.columName;
      this.form.propkey = selected.columkey;
    },
    //添加列
    sumbitConlum() {
      const newProp = this.form.propkey
      const newLabel = this.form.propName

      // 添加新列配置
      this.dynamicColumns.push({
        prop: newProp,
        label: newLabel,
      })

      // 为每行数据添加新列对应的属性
      this.rwhj.forEach(item => {
        this.$set(item, newProp, "")
      })
      this.dialogTableVisible = false

      this.columnIndex++

      // 提示用户
      this.$message.success(`已添加新列: ${newLabel}`)

    },

    //任务兵力舰艇添加行
    addNewRow51() {
      this.jtbl.push({
        xvhao: undefined,
        lx: "",
        xinghao: "",
        xjh: "",
        ms: "",
        bz: "",
      })
    },
    addNewRow52() {
      this.zsjbl.push({
        xvhao: undefined,
        lx: "",
        xh: "",
        xjh: "",
        ms: "",
        bz: ""
      })
    },
    //通信载荷
    addNewRow71() {
      this.txzh.push({
        txfs: "",
        txzb: "",
        bz: ""
      })
    },
    //探测载荷
    addNewRow72() {
      this.tczh.push({
        tcsb: "",
        tczb: "",
        bz: ""
      })
    },
    //攻击载荷
    addNewRow73() {
      this.gjzh.push({
        wqlx: "",
        wqzb: "",
        bz: ""
      })
    },


    goInfo(info) {
      console.log(info)
      this.$router.push('/' + info)
    },

    //起降图谱
    getQj() {
      var graphUse = [];
      this.showTp1 = true;
      graphUse.push("风");
      graphUse.push("降水");
      graphUse.push("云雾");
      graphUse.push("积冰");
      graphUse.push("雷暴");
      this.getInfoGraph(graphUse);

    },
    getFx() {
      var graphUse = [];
      this.showTp2 = true;

      graphUse.push("相对风");
      graphUse.push("云底高");
      graphUse.push("能见度");
      graphUse.push("海况");
      this.getInfoGraph2(graphUse);
    },
    getTxzh() {
      var graphUse = [];
      this.showTp3 = true;
      for (let a = 0; a < this.txzh.length; a++) {
        if (this.txzh[a].txfs.indexOf("短波") != -1) {
          graphUse.push("电离层")
        }
        if (this.txzh[a].txfs.indexOf("超短波") != -1) {
          graphUse.push("大气波导")
        }
      }
      this.getInfoGraph3(graphUse);

    },

    getTczh() {
      var graphUse = [];
      this.showTp4 = true;
      for (let a = 0; a < this.tczh.length; a++) {
        if (this.tczh[a].tcsb.indexOf("吊放声呐") != -1) {
          graphUse.push("声速剖面")
          graphUse.push("海况")
          graphUse.push("海流")
          graphUse.push("海底地形")
          graphUse.push("海底底质")
        }
        if (this.tczh[a].tcsb.indexOf("声呐浮标") != -1) {
          graphUse.push("声速剖面")
          graphUse.push("海况")
          graphUse.push("海流")
          graphUse.push("海底地形")
          graphUse.push("海底底质")
        }
        if (this.tczh[a].tcsb.indexOf("机载雷达") != -1) {
          graphUse.push("降水")
          graphUse.push("降雨")
          graphUse.push("降雪")
          graphUse.push("冰雹")
          graphUse.push("云雾")
          graphUse.push("海杂波")
          graphUse.push("大气波导")
          graphUse.push("电磁干扰")
        }
      }
      this.getInfoGraph4(graphUse);

    },

    getGjzh() {
      var graphUse = [];
      this.showTp5 = true;
      for (let a = 0; a < this.gjzh.length; a++) {
        if (this.gjzh[a].wqzb.indexOf("鱼雷") != -1) {
          graphUse.push("海况")
          graphUse.push("海深")
          graphUse.push("海底地质")
          graphUse.push("海底混响")
          graphUse.push("海面混响")
        }
        if (this.gjzh[a].wqzb.indexOf("导弹") != -1) {
          graphUse.push("倒角遮挡")
          graphUse.push("大气波导")
          graphUse.push("海况")
          graphUse.push("降雨")
          graphUse.push("云雾")
          graphUse.push("电磁干扰")
        }
      }
      this.getInfoGraph5(graphUse);

    },


    //图谱1获取
    getInfoGraph(graphUse) {
      this.graphData = undefined;
      this.demoData = {}

      let uniqueArray = graphUse.filter((item, index) => graphUse.indexOf(item) === index);
      let params = {
        keywords: uniqueArray
      };
      getDomainGraphNew1(params).then((res) => {
        if (res.data.nodes.length != 0) {
          this.zhengl(res.data);
        }

      })

    },
    //图谱1整理
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
              label: nodeList[a].name,
              shape: 'circle',
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,
              },
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 3) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 2) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
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


              headTipText: "附加信息",
              ...style, // 展开 style 对象以应用样式属性

            });
          }


        }
      }

      // var allOne = nodeList[0].docId


      if (lineList != undefined) {
        for (let b = 0; b < lineList.length; b++) {

          var bbb = { name: lineList[b].relate }
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
    useJs(row) {
      var data = {
        name: row.name
      }
      if (row.name == "XXXX辅助决策") {
        data.jsInfo = "QJFXT"
      } else if (row.name == "大气降水对雷达探测的影响分析软件") {
        data.jsInfo = "DQJS"
      } else if (row.name == "大气波导对电磁场传播的影响分析软件") {
        data.jsInfo = "LDWLT"
      } else if (row.name == "海洋环境对声呐探测的影响分析软件") {
        data.jsInfo = "SN1"
      } else if (row.name == "声呐探测距离估算软件") {
        data.jsInfo = "SNJS"
      } else if (row.name == "电离层对短波通信的影响软件") {
        data.jsInfo = "DBDLC"
      } else if (row.name == "舰载直升机航空鱼雷作战使用辅助决策") {
        data.jsInfo = "YLDQGJ"
      } else if (row.name == "舰载直升机空舰导弹导弹作战使用辅助决策") {
        data.jsInfo = "DDZZSYFZJC"
      } else if (row.name == "面向舰机超短波通信的表面波导可用性评估软件") {
        data.info = "CDBTX"
      }
      getJsList(data).then((res) => {
        this.jsId = res.data.list[0].id;
        console.log(res)
        var jsInfo = res.data.list[0].jsInfo;
        if (jsInfo == "QJFXT") {
          this.showQjJs = true;
        } else if (jsInfo == "DQJS") {
          this.showDQJs = true;
        } else if (jsInfo == "SNJS") {
          this.showSNJs = true;
        } else if (jsInfo == "SN1") {
          this.showSN1Js = true;
        } else if (jsInfo == "JSGL") {
          this.showJSJs = true;
        } else if (jsInfo == "DBDLC") {
          this.showDBJs = true;
        } else if (jsInfo == "YLDQGJ") {
          this.showYLJs = true;
        } else if (jsInfo == "DDZZSYFZJC") {
          this.showDDZZJs = true;
        } else if (jsInfo == "LDWLT") {
          this.showLDJS = true;
        } else if (jsInfo == "CDBTX") {
          this.showCDBJS = true;
        }
      })
      console.log(row)
    },
    getNodeStyle(group) {
      const styles = [
        { size: 450, width: 450, height: 450, color: '255,111,62', font: 'normal 68px Arial', fontColor: '255,255,255' },
        { size: 350, width: 350, height: 350, color: '255,163,132', font: 'normal 68px Arial', fontColor: '255,255,255' },
        { size: 300, width: 300, height: 300, color: '0,246,255', font: 'normal 50px Arial', fontColor: '0,0,0' },
        { size: 250, width: 250, height: 250, color: '0,198,255', font: 'normal 40px Arial', fontColor: '0,0,0' },
        { size: 200, width: 200, height: 200, color: '42,152,255', font: 'normal 32px Arial', fontColor: '255,255,255' },
        { size: 150, width: 150, height: 150, color: '0,95,183', font: 'normal 30px Arial', fontColor: '0,0,0' },
        { size: 130, width: 130, height: 130, color: '0,62,164', font: 'normal 28px Arial', fontColor: '255,255,255' }
      ];

      return styles[group] || {};
    },
    getNodeStyle1(group) {
      const styles = [
        { size: 450, width: 450, height: 450 },
        { size: 350, width: 350, height: 350 },
        { size: 300, width: 300, height: 300 },
        { size: 250, width: 250, height: 250 },
        { size: 200, width: 200, height: 200 },
        { size: 150, width: 150, height: 150 },
        { size: 130, width: 130, height: 130 }
      ];

      return styles[group] || {};
    },
    async drawGraphData() {
      this.graphData = this.demoData;
      if (this.visGraph === null) {
        this.createGraph();

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
        }
      };

      this.visGraph = new VisGraph(document.getElementById('graph-panel'), configWithEvents);
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


    //图谱1获取
    getInfoGraph2(graphUse) {
      this.graphData1 = undefined;
      this.demoData1 = {}


      let uniqueArray = graphUse.filter((item, index) => graphUse.indexOf(item) === index);
      let params = {
        keywords: uniqueArray
      };
      console.log("-----------")
      getDomainGraphNew1(params).then((res) => {
        if (res.data.nodes.length != 0) {
          this.zhengl2(res.data);
        }

      })

      // if (this.keywords1 != '' && this.keywords1 != undefined) {
      //   // this.visGraph.clearAll();
      //   let params = {
      //     nodename: this.keywords1,
      //   };
      //   getgraphInfo(params).then((res) => {
      //     this.zhengl2(res.data);
      //   })
      // } else {
      //
      //   let params = {};
      //   getgraphInfo(params).then((res) => {
      //     this.zhengl2(res.data);
      //   })
      // }
    },
    //图谱1整理
    zhengl2(data) {
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
              label: nodeList[a].name,
              shape: 'circle',
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,
              },
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 3) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 2) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
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


              headTipText: "附加信息",
              ...style, // 展开 style 对象以应用样式属性

            });
          }


        }
      }

      // var allOne = nodeList[0].docId


      if (lineList != undefined) {
        for (let b = 0; b < lineList.length; b++) {

          var bbb = { name: lineList[b].relate }
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


      this.demoData1 = {
        "nodes": nodes,
        "links": links
      }
      this.drawGraphData2();
    },
    async drawGraphData2() {
      this.graphData1 = this.demoData1;
      if (this.visGraph1 === null) {
        this.createGraph2();

        this.visGraph1.drawData(this.graphData1);
        this.visGraph1.incremaNodesCodinate(this.graphData1.nodes);
        this.reLayout2();
      } else {
        this.createGraph2();
        this.visGraph1.drawData(this.graphData1);
        this.visGraph1.incremaNodesCodinate(this.graphData1.nodes);
        this.reLayout2();
      }
      this.loading = false;
    },
    // 创建全局绘图客户端对象
    createGraph2() {
      const configWithEvents = {
        ...this.config,
        node: {
          ...this.config.node,
        }
      };

      this.visGraph1 = new VisGraph(document.getElementById('graph-panel1'), configWithEvents);
    },
    // 执行布局算法
    reLayout2(alpha) {
      var that = this;
      if (alpha == null) {
        that.visLayout = null;
        that.visLayout = new LayoutFactory(this.visGraph1.getGraphData()).createLayout('fastFR');
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
          size: [that.visGraph1.stage.width, that.visGraph1.stage.height]
        });
      } else {
        that.visLayout.alpha += (alpha > 1 ? 0.2 : alpha); //继续运动
      }

      runLayout();//开始继续动画执行

      //通过动画帧控制控制布局算法的执行，有动画效果
      function runLayout() {
        cancelAnimationFrame(that.layoutLoopName);//停止动画控制
        that.visLayout.runLayout();  //运行布局算法
        that.visGraph1.refresh();
        if (that.visLayout.alpha > 0.05) {
          that.layoutLoopName = requestAnimationFrame(runLayout);
        } else {
          if (that.visGraph1.currentNode && that.visGraph1.currentNode.isDragging) {
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


    //图谱3获取
    getInfoGraph3(graphUse) {
      this.graphData2 = undefined;
      this.demoData2 = {}
      let uniqueArray = graphUse.filter((item, index) => graphUse.indexOf(item) === index);
      let params = {
        keywords: uniqueArray
      };
      console.log("-----------")
      getDomainGraphNew1(params).then((res) => {
        if (res.data.nodes.length != 0) {
          this.zhengl3(res.data);
        }

      })
    },
    //图谱1整理
    zhengl3(data) {
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
              label: nodeList[a].name,
              shape: 'circle',
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,
              },
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 3) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 2) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
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


              headTipText: "附加信息",
              ...style, // 展开 style 对象以应用样式属性

            });
          }


        }
      }

      // var allOne = nodeList[0].docId


      if (lineList != undefined) {
        for (let b = 0; b < lineList.length; b++) {

          var bbb = { name: lineList[b].relate }
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


      this.demoData2 = {
        "nodes": nodes,
        "links": links
      }
      this.drawGraphData3();
    },
    async drawGraphData3() {
      this.graphData2 = this.demoData2;
      if (this.visGraph2 === null) {
        this.createGraph3();

        this.visGraph2.drawData(this.graphData2);
        this.visGraph2.incremaNodesCodinate(this.graphData2.nodes);
        this.reLayout3();
      } else {
        this.createGraph3();
        this.visGraph2.drawData(this.graphData2);
        this.visGraph2.incremaNodesCodinate(this.graphData2.nodes);
        this.reLayout3();
      }
      this.loading = false;
    },
    // 创建全局绘图客户端对象
    createGraph3() {
      const configWithEvents = {
        ...this.config,
        node: {
          ...this.config.node,
        }
      };

      this.visGraph2 = new VisGraph(document.getElementById('graph-panel2'), configWithEvents);
    },
    // 执行布局算法
    reLayout3(alpha) {
      var that = this;
      if (alpha == null) {
        that.visLayout = null;
        that.visLayout = new LayoutFactory(this.visGraph2.getGraphData()).createLayout('fastFR');
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
          size: [that.visGraph2.stage.width, that.visGraph2.stage.height]
        });
      } else {
        that.visLayout.alpha += (alpha > 1 ? 0.2 : alpha); //继续运动
      }

      runLayout();//开始继续动画执行

      //通过动画帧控制控制布局算法的执行，有动画效果
      function runLayout() {
        cancelAnimationFrame(that.layoutLoopName);//停止动画控制
        that.visLayout.runLayout();  //运行布局算法
        that.visGraph2.refresh();
        if (that.visLayout.alpha > 0.05) {
          that.layoutLoopName = requestAnimationFrame(runLayout);
        } else {
          if (that.visGraph2.currentNode && that.visGraph2.currentNode.isDragging) {
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


    //图谱4获取
    getInfoGraph4(graphUse) {
      this.graphData3 = undefined;
      this.demoData3 = {}

      let uniqueArray = graphUse.filter((item, index) => graphUse.indexOf(item) === index);
      let params = {
        keywords: uniqueArray
      };

      getDomainGraphNew1(params).then((res) => {
        if (res.data.nodes.length != 0) {
          this.zhengl4(res.data);
        }

      })
    },
    //图谱1整理
    zhengl4(data) {
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
              label: nodeList[a].name,
              shape: 'circle',
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,
              },
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 3) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 2) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
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


              headTipText: "附加信息",
              ...style, // 展开 style 对象以应用样式属性

            });
          }


        }
      }
      if (lineList != undefined) {
        for (let b = 0; b < lineList.length; b++) {

          var bbb = { name: lineList[b].relate }
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
      this.demoData3 = {
        "nodes": nodes,
        "links": links
      }
      this.drawGraphData4();
    },
    async drawGraphData4() {
      this.graphData3 = this.demoData3;
      if (this.visGraph3 === null) {
        this.createGraph4();

        this.visGraph3.drawData(this.graphData3);
        this.visGraph3.incremaNodesCodinate(this.graphData3.nodes);
        this.reLayout4();
      } else {
        this.createGraph4();
        this.visGraph3.drawData(this.graphData3);
        this.visGraph3.incremaNodesCodinate(this.graphData3.nodes);
        this.reLayout4();
      }
      this.loading = false;
    },
    // 创建全局绘图客户端对象
    createGraph4() {
      const configWithEvents = {
        ...this.config,
        node: {
          ...this.config.node,
        }
      };

      this.visGraph3 = new VisGraph(document.getElementById('graph-panel3'), configWithEvents);
    },
    // 执行布局算法
    reLayout4(alpha) {
      var that = this;
      if (alpha == null) {
        that.visLayout = null;
        that.visLayout = new LayoutFactory(this.visGraph3.getGraphData()).createLayout('fastFR');
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
          size: [that.visGraph3.stage.width, that.visGraph3.stage.height]
        });
      } else {
        that.visLayout.alpha += (alpha > 1 ? 0.2 : alpha); //继续运动
      }

      runLayout();//开始继续动画执行

      //通过动画帧控制控制布局算法的执行，有动画效果
      function runLayout() {
        cancelAnimationFrame(that.layoutLoopName);//停止动画控制
        that.visLayout.runLayout();  //运行布局算法
        that.visGraph3.refresh();
        if (that.visLayout.alpha > 0.05) {
          that.layoutLoopName = requestAnimationFrame(runLayout);
        } else {
          if (that.visGraph3.currentNode && that.visGraph3.currentNode.isDragging) {
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


    //图谱5获取
    getInfoGraph5(graphUse) {
      this.graphData4 = undefined;
      this.demoData4 = {}

      let uniqueArray = graphUse.filter((item, index) => graphUse.indexOf(item) === index);
      let params = {
        keywords: uniqueArray
      };

      getDomainGraphNew1(params).then((res) => {
        if (res.data.nodes.length != 0) {
          this.zhengl5(res.data);
        }

      })
    },
    //图谱5整理
    zhengl5(data) {
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
              label: nodeList[a].name,
              shape: 'circle',
              properties: {
                name: nodeList[a].name,
                docId: nodeList[a].docId,
                parent: allOne,
                leve: nodeList[a].group,
                type: nodeList[a].type,
              },
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 3) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
              ...style1, // 展开 style 对象以应用样式属性

            });
          } else if (nodeList[a].type == 2) {
            const style1 = this.getNodeStyle1(parseInt(nodeList[a].group, 10))
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
              image: "http://127.0.0.1:10035/profile/head41.jpg",
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


              headTipText: "附加信息",
              ...style, // 展开 style 对象以应用样式属性

            });
          }


        }
      }
      if (lineList != undefined) {
        for (let b = 0; b < lineList.length; b++) {

          var bbb = { name: lineList[b].relate }
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
      this.demoData4 = {
        "nodes": nodes,
        "links": links
      }
      this.drawGraphData5();
    },
    async drawGraphData5() {
      this.graphData4 = this.demoData4;
      if (this.visGraph4 === null) {
        this.createGraph5();

        this.visGraph4.drawData(this.graphData4);
        this.visGraph4.incremaNodesCodinate(this.graphData4.nodes);
        this.reLayout5();
      } else {
        this.createGraph5();
        this.visGraph4.drawData(this.graphData4);
        this.visGraph4.incremaNodesCodinate(this.graphData4.nodes);
        this.reLayout5();
      }
      this.loading = false;
    },
    // 创建全局绘图客户端对象
    createGraph5() {
      const configWithEvents = {
        ...this.config,
        node: {
          ...this.config.node,
        }
      };

      this.visGraph4 = new VisGraph(document.getElementById('graph-panel4'), configWithEvents);
    },
    // 执行布局算法
    reLayout5(alpha) {
      var that = this;
      if (alpha == null) {
        that.visLayout = null;
        that.visLayout = new LayoutFactory(this.visGraph4.getGraphData()).createLayout('fastFR');
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
          size: [that.visGraph4.stage.width, that.visGraph4.stage.height]
        });
      } else {
        that.visLayout.alpha += (alpha > 1 ? 0.2 : alpha); //继续运动
      }

      runLayout();//开始继续动画执行

      //通过动画帧控制控制布局算法的执行，有动画效果
      function runLayout() {
        cancelAnimationFrame(that.layoutLoopName);//停止动画控制
        that.visLayout.runLayout();  //运行布局算法
        that.visGraph4.refresh();
        if (that.visLayout.alpha > 0.05) {
          that.layoutLoopName = requestAnimationFrame(runLayout);
        } else {
          if (that.visGraph4.currentNode && that.visGraph4.currentNode.isDragging) {
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


  },
  mounted() {
    this.docId = this.$route.query.id;
    this.userType = localStorage.getItem("type");
    this.userName = localStorage.getItem("name");
    this.getTable()
    // this.historyJsTest()
    // this.getAllJs()

  },
  watch: {
    'gzType'(newVal) {
      this.gzInfoType = "";
      this.gzInfoType1 = "";
      if (newVal == '起降') {
        this.yjgzTypeList = [{
          id: 1,
          value: '云',
          label: '云'
        },
        {
          id: 2,
          value: '能见度',
          label: '能见度'
        },
        {
          id: 3,
          value: '风',
          label: '风'
        },
        {
          id: 4,
          value: '舰船摇荡',
          label: '舰船摇荡'
        }]
      } else if (newVal == '飞行') {
        this.yjgzTypeList = [{
          id: 1,
          value: '气温',
          label: '气温'
        },
        {
          id: 2,
          value: '飞机积冰',
          label: '飞机积冰'
        },
        {
          id: 3,
          value: '风',
          label: '风'
        },
        {
          id: 4,
          value: '积雨云',
          label: '积雨云'
        },]
      } else if (newVal == '探测') {
        this.yjgzTypeList = [{
          id: 1,
          value: '雷达',
          label: '雷达'
        },
        {
          id: 2,
          value: '声呐',
          label: '声呐'
        }]
      } else if (newVal == '通信') {
        this.yjgzTypeList = [{
          id: 1,
          value: '短波',
          label: '短波'
        },
        {
          id: 2,
          value: '超短波',
          label: '超短波'
        }]
      } else {
        this.yjgzTypeList = [{
          id: 1,
          value: '航空鱼雷',
          label: '航空鱼雷'
        },
        {
          id: 2,
          value: '空舰导弹',
          label: '空舰导弹'
        }]
      }

    },
    'gzInfoType'(newVal) {
      this.gzInfoType1 = "";
      if (newVal == '雷达') {
        this.ejgzTypeList = [{
          id: 1,
          value: '探测距离',
          label: '探测距离'
        },
        {
          id: 2,
          value: '大气衰减',
          label: '大气衰减'
        },
        {
          id: 3,
          value: '海杂波',
          label: '海杂波'
        }]
      } else if (newVal == '声呐') {
        this.ejgzTypeList = [{
          id: 1,
          value: '声速剖面',
          label: '声速剖面'
        },
        {
          id: 2,
          value: '海况',
          label: '海况'
        },
        {
          id: 3,
          value: '海流',
          label: '海流'
        },
        {
          id: 4,
          value: '内波',
          label: '内波'
        },
        {
          id: 5,
          value: '海洋锋',
          label: '海洋锋'
        },
        {
          id: 6,
          value: '中尺度涡',
          label: '中尺度涡'
        }]
      } else if (newVal == '航空鱼雷') {
        this.ejgzTypeList = [{
          id: 1,
          value: '空中下落段',
          label: '空中下落段'
        },
        {
          id: 2,
          value: '下潜寻深段',
          label: '下潜寻深段'
        },
        {
          id: 3,
          value: '搜索段',
          label: '搜索段'
        },
        {
          id: 4,
          value: '跟踪段',
          label: '跟踪段'
        }]
      } else if (newVal == '空舰导弹') {
        this.ejgzTypeList = [{
          id: 1,
          value: '直升机突防',
          label: '直升机突防'
        },
        {
          id: 2,
          value: '导弹弹道',
          label: '导弹弹道'
        },
        {
          id: 3,
          value: '导弹末制导',
          label: '导弹末制导'
        }]
      } else {
        this.ejgzTypeList = [];
      }
    },
    'task'(newVal) {
      if (newVal == "对潜攻击") {
        this.tczhs = [{
          value: '机载雷达',
          label: '机载雷达'
        }]
        this.gjzhs = [{
          value: '航空鱼雷',
          label: '航空鱼雷'
        }]
      }
      if (newVal == "对海攻击（反舰）") {
        this.tczhs = [{
          value: '机载雷达',
          label: '机载雷达'
        },
        {
          value: '光电探头',
          label: '光电探头'
        }]
        this.gjzhs = [{
          value: '航空导弹',
          label: '航空导弹'
        }]
      }
      if (newVal == "预警侦察") {
        this.tczhs = [{
          value: '机载雷达',
          label: '机载雷达'
        }]
        this.gjzhs = []
      }
    },
    'ship'(newVal) {
      if ((newVal == "驱052D" || newVal == "护054A") && (this.task == "对潜攻击" || this.task == "对潜搜索")) {
        this.planes = [{
          value: '直9F',
          label: '直9F'
        },
        {
          value: '卡28',
          label: '卡28'
        }]
      } else if ((this.task == "对潜攻击" || this.task == "对潜搜索") && newVal == "驱055") {
        this.planes = [{
          value: '直9F',
          label: '直9F'
        },
        {
          value: '直20',
          label: '直20'
        }]
      } else if (this.task == "对海攻击（反舰）" && (newVal == "驱052D" || newVal == "护054A")) {
        this.planes = [{
          value: '直9D',
          label: '直9D'
        }]
      } else if (this.task == "对海攻击（反舰）" && newVal == "驱055") {
        this.planes = [{
          value: '直9D',
          label: '直9D'
        },
        {
          value: '直20',
          label: '直20'
        }]
      } else if (this.task == "预警侦查" && (newVal == "驱052D" || newVal == "护054A")) {
        this.planes = [{
          value: '直9D',
          label: '直9D'
        },
        {
          value: '直9F',
          label: '直9F'
        },
        {
          value: '卡28',
          label: '卡28'
        }]
      } else if (this.task == "预警侦查" && newVal == "驱055") {
        this.planes = [{
          value: '直9D',
          label: '直9D'
        },
        {
          value: '直9F',
          label: '直9F'
        },
        {
          value: '直20',
          label: '直20'
        }]
      }
    },
    plane(newVal) {
      if ((newVal == "直20" || newVal == "卡28") && this.task == "对潜搜索") {
        this.tczhs = [{
          value: '机载雷达',
          label: '机载雷达'
        },
        {
          value: '吊放声呐',
          label: '吊放声呐'
        },
        {
          value: '声呐浮标',
          label: '声呐浮标'
        }]
        this.gjzhs = []
      } else if (newVal == "直9F" && this.task == "对潜搜索") {
        this.options5 = [{
          value: '机载雷达',
          label: '机载雷达'
        },
        {
          value: '吊放声呐',
          label: '吊放声呐'
        }]
        this.options6 = []
      }
    }
  },
}
</script>
<style scoped>
/* * {
  margin: 0;
  padding: 0;
} */

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

.contentInfo {
  width: 95%;
  height: 90%;
  margin-left: 2.5%;
  margin-top: 2.5%;
  color: #Ffffff;
  overflow-y: scroll;
  overflow-x: hidden;
}

.contentInfo::-webkit-scrollbar {
  width: 0.5vw;
  height: 0.5vw;
}

.contentInfo::-webkit-scrollbar-track {
  background: transparent;
}

.contentInfo::-webkit-scrollbar-thumb {
  background: rgba(51, 216, 255);
  border-radius: 0.5vw;
}

.contentInfo::-webkit-scrollbar-thumb:hover {
  background: rgba(51, 216, 255);
}


.contentInfo::v-deep(.has-gutter th) {

  font-weight: bold;
  /* 加粗表头文字 */

  color: #FFFFFF;
}

.contentInfo::v-deep(.el-table tr) {
  background-color: transparent;
}

.contentInfo::v-deep(.el-textarea__inner) {
  background-color: transparent;
  border: none;
}

.contentInfo::v-deep(.el-table) {
  background-color: transparent;
}

.contentInfo::v-deep(.el-table th.el-table__cell) {
  background-color: transparent;
  border: none;
}

.contentInfo::v-deep(.el-table--border::after) {
  background-color: transparent;
}

.contentInfo::v-deep(.el-table td.el-table__cell, .el-table th.el-table__cell) {
  border: none;
}

.contentInfo::v-deep(.el-table::before) {
  background-color: transparent;
}

.contentInfo::v-deep(.el-button) {
  font-size: 0.8vw;
  padding: -1vw 2vw;
}

.contentInfo::v-deep(.el-table__header) {
  background-color: #00a1ff94;
  border-radius: 2vw;
}

.contentInfo::v-deep(.el-table thead) {
  color: #FFFFFF;
}


::v-deep(.el-textarea) {
  background-image: url("../assets/img/bgbg.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;

}

::v-deep(.el-textarea textarea) {
  color: #FFFFFF;
  font-size: 1vw;

}

.contentBox1 {
  height: 10%;
  width: 100%;
  margin-bottom: 2%;
}

.inputBao {
  width: 90%;
  height: 5vw;
  margin-left: 5%;
  position: relative;
}

.contentBox2 {
  height: 20%;
  width: 100%;
  margin-bottom: 2%;
}

.contentBox3 {
  height: 10%;
  width: 100%;
  margin-bottom: 2%;
}

.contentBox4 {
  height: 36%;
  width: 100%;
  margin-bottom: 2%;
}

.contentBox4 {
  width: 100%;
  margin-bottom: 2%;
}

.contentBox6 {
  height: 20%;
  width: 100%;
  margin-bottom: 2%;
}

.contentBox7 {
  height: 20%;
  width: 100%;
  margin-bottom: 2%;
}

::v-deep(.el-textarea__inner) {
  min-height: 1vw !important;
}


.contentBox3::v-deep(.el-input__inner) {
  background-color: transparent;
  background-image: url("@/assets/img/timebg.png");
  background-size: 100% 100%;
  border: none;
  color: #FFFFFF;

}

.contentBox3::v-deep(.el-input__icon) {
  color: #FFFFFF;
}

/* 侧边栏样式 */
.sidebar-toggle {
  position: fixed;
  right: 0;
  top: 5%;
  width: 2vw;
  height: 4vw;
  background-color: transparent;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  z-index: 9998;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
}

.sidebar-toggle img {
  width: 1.5vw;
  height: auto;
}

.sidebar {
  position: fixed;
  top: 0;
  right: -16vw;
  width: 10vw;
  height: 100%;
  background-image: url("../assets/img/bwjktupm.png");
  background-size: 100% 100%;
  background-position: left top;
  background-repeat: no-repeat;
  transition: right 0.3s ease-in-out;
  z-index: 9999;
  color: white;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.sidebar-visible {
  right: 0;
}

.sidebar-header {
  height: 4vw;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 0 0 2vw;
  border-bottom: none;
  /* 移除边框线 */
  width: calc(100% - 2vw);
}

.sidebar-close {
  cursor: pointer;
  width: 2vw;
  height: 2vw;
  display: flex;
  justify-content: center;
  align-items: center;
}

.sidebar-close img {
  width: 1.5vw;
  height: auto;
}

.sidebar-content {

  overflow-y: auto;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  width: 86%;
  margin-left: 14%;
  height: 60%;
}

.sidebar-item {
  padding: 1.2vw 0;
  margin: 0;
  border-bottom: none;
  /* 移除边框线 */
  cursor: pointer;
  transition: background-color 0.2s;
  text-align: center;

  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.9vw;
  width: 100%;
}

.sidebar-item:hover {
  background-image: url("../assets/img/xmtk.png");
  background-color: rgba(255, 255, 255, 0.08);
}


.sidebar-item-active {

  background-size: 100% 100%;
  background-position: right;
  background-repeat: no-repeat;
  color: #13ffff;
  position: relative;
  width: 100%;
  padding-right: 0;
}


.sidebar-item-active::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 0.3vw;
  height: 100%;
  background-color: #13ffff;
}

.showList {
  width: 23vw;
  height: 30vw;
  background-image: url("../assets/img/gzbg.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  position: absolute;
  right: 8vw;
  z-index: 3000;
  padding: 1vw 0vw;
  overflow-y: scroll;
}

.showList::-webkit-scrollbar {
  width: 0.5vw;
  height: 0.5vw;
}

.showList::-webkit-scrollbar-track {
  background: transparent;
}

.showList::-webkit-scrollbar-thumb {
  background: rgba(51, 216, 255);
  border-radius: 0.5vw;
}

.showList::-webkit-scrollbar-thumb:hover {
  background: rgba(51, 216, 255);
}

.showList::v-deep(.el-table tr) {
  background-color: transparent;
}

.showList::v-deep(.el-textarea__inner) {
  background-color: transparent;
  border: none;
}

.showList::v-deep(.el-table) {
  background-color: transparent;
}

.showList::v-deep(.el-table th.el-table__cell) {
  background-color: transparent;
  border: none;
}

.showList::v-deep(.el-table--border::after) {
  background-color: transparent;
}

.showList::v-deep(.el-table td.el-table__cell, .el-table th.el-table__cell) {
  border: none;

}

.showList::v-deep(.el-table::before) {
  background-color: transparent;
}

.showList::v-deep(.el-table th.el-table__cell .cell) {
  line-height: 16px;
}

.showList::v-deep(.el-table__header) {
  background-color: #ffffff63;
}

.showList::v-deep(.el-table thead) {
  color: #FFFFFF;
}

.testInfo::v-deep(.w-e-image-container>img) {
  width: 4vw !important;
  object-fit: contain;
  float: left;
}

.testInfo /deep/.w-e-text-container {
  background-color: transparent !important;
  color: #fff;
}

::v-deep(.testInfo) {
  background-image: url("../assets/img/baoGaoInput.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;

}

/* .bg {
  background-image: url("../assets/img/bkbg.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
} */

.showList .el-table {
  color: #fff;
}

/deep/.w-e-image-container {
  width: auto !important;
}

.el-dialog__body .w-e-text-container {
  width: 15vw;
}

/deep/.el-dialog {
  margin-top: 6vh !important;
  width: 82% !important;
  height: 87% !important;
}

/deep/.el-dialog__body {
  height: 94.5% !important;
  padding: 0px;
  display: flex;
  flex-direction: column;
  z-index: 9999;
}

.qjfxt {
  background: transparent;
}

.el-select {
  margin-right: 6vw;
  margin-bottom: 2vh;
}

.input {
  width: 20%;
  margin-right: 2.5vw;
  margin-bottom: 2vh;
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.bg /deep/.el-input__inner {
  background-color: transparent;
  color: #fff;
  border: none;
  text-align: center;
}

.contentBox4 .el-input {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.contentBox5 .el-input {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.bg .el-input {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.head {
  //margin-left: 3.4vw;
  background-image: url("@/assets/img/graphInput.png");
  background-repeat: no-repeat;
  background-size: 100% 100%;
}




/deep/.el-input__inner {
  border: none;
  background-color: transparent !important;
  color: #fff
}

.el-table /deep/th.el-table__cell.is-leaf {
  border: none;
  background-color: transparent;
}

.selectBg {
  background-image: url("@/assets/img/graphInput.png");
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.inputBg {
  background-image: url("@/assets/img/graphInputNew.png");
  background-repeat: no-repeat;
  background-size: cover;
  width: 90%;
  margin-left: 3vw;
}

.el-table /deep/.cell {
  color: #fff
}

.el-dialog .el-table /deep/.cell {
  color: #000
}

:deep(.head .el-input__inner::placeholder) {
  color: white !important;
  opacity: 1;
}

:deep(.selectBg .el-input__inner::placeholder) {
  color: white !important;
  opacity: 1;
}

:deep(.input .el-input__inner::placeholder) {
  color: white !important;
  opacity: 1;
}

:deep(.el-table--enable-row-hover .el-input__inner::placeholder) {
  color: white !important;
  opacity: 1;
}

:deep(.el-table--enable-row-hover .el-table__body tr:hover>td) {
  background-color: transparent !important;
}

:deep(.el-table tr) {
  background-color: transparent;
}


.history:deep(.el-dialog__title) {
  font-size: 1.2vw !important;
  /* 标题字体大小 */
  color: #000000 !important;
}


.history /deep/.el-dialog__body {
  background-color: #006cda;
  padding-left: 2%;
  display: block;
  height: 81vh;
  overflow-y: scroll;
}

/deep/ .el-dialog__body::-webkit-scrollbar {
  width: 0.4vw;
  height: 0.4vw;
}

/deep/ .el-dialog__body::-webkit-scrollbar-track {
  background: transparent;
}

/deep/ .el-dialog__body::-webkit-scrollbar-thumb {
  background: rgba(51, 216, 255);
  border-radius: 0.4vw;
}

/deep/ .el-dialog__body::-webkit-scrollbar-thumb:hover {
  background: rgba(51, 216, 255);
}

.dialog1 /deep/.el-dialog__body {
  padding-left: 2%;
  padding-right: 2%;
}


.dialog1 /deep/.el-input__inner {
  color: #050505;
  border: 1px solid black;
  text-align: center;
}

.dialog1 /deep/.el-dialog {
  margin-top: 8vh !important;
  width: 82% !important;
  height: 64% !important;
}


.graphcontains1 {
  width: 40%;
  height: 2vw;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-left: 1%;
}

.graphcontains2 {
  width: 40%;
  height: 2vw;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-left: 1%;
  margin-bottom: 1vh;
}

.custom-select {
  position: relative;
  width: 15vw;
  cursor: pointer;
  height: 85%;
  line-height: 1.5vw;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-left: 3.5vw;
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
  display: flex;
  flex-direction: column;
  z-index: 100;
}

.options::-webkit-scrollbar {
  width: 0.4vw;
  height: 0.4vw;
}

.options::-webkit-scrollbar-track {
  background: transparent;
}

.options::-webkit-scrollbar-thumb {
  background: rgba(51, 216, 255);
  border-radius: 0.4vw;
}

.options::-webkit-scrollbar-thumb:hover {
  background: rgba(51, 216, 255);
}

.selected-option {
  text-align: center;
  line-height: 1.7vw;
  width: 7vw;
}

.option {
  display: flex;
  justify-content: center;
}

::v-deep .el-input__inner::placeholder {
  color: #fff;
}

.el-date-editor.el-input {
  background-color: rgba(0, 161, 255, 0.58);
  border-radius: 1vw;
}

.selectPlace /deep/.el-input__inner::placeholder {
  color: #fff !important;
}

.el-dialog .el-table /deep/.cell {
  color: #fff;
}

.nameInput {
  background-image: url("../assets/img/baoGaoInput.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}

.divBg {
  background-color: rgba(125, 164, 200, 0.51);
}
</style>
