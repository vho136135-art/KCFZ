<template>
  <div class="background-container">
    <div class="content-container" id="capture">
      <div
          style="display: flex;width: 100%;margin-bottom: 1vh;margin-top: 2vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color: #004e9c; font-size: 1.6vw;font-weight: 500;">
          电离层对短波通信的影响分析软件
        </div>

      </div>
      <img style="height: 0.15vw;object-fit: contain;" src="@/assets/img/hengxian.png">
      <div style="width: 94%;display: flex;flex-direction: row;height: 60%;margin-left: 3%;margin-top: 1%;">
        <div class="imgBox" style="display: flex;justify-content: center;">
          <div id="chart-container" style="width: 70%;margin-left: -20%;"></div>
        </div>
        <div style="width: 18%;height: 100%;background-color: #006cda;margin-left: 3%">
          <div
              style="width: 100%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 0.8%;">
            仿真控制
          </div>

          <div style="width: 100%;height: 90%;display: flex;flex-direction:column;margin-top: 2%;margin-left: 6%;">
            <div class="buttonLeft" style="display: inline-block;margin-left:1vw;width: 11vw;margin-top: 8%;">
              <el-button style="font-size: 0.8vw;" @click="test">载入测试值</el-button>
            </div>
            <div class="buttonRight" style="width: 11vw;display: inline-block;margin-top: 8%;">
              <el-button style="font-size: 0.8vw;margin-left: -1vw;" @click="dataInitialize">数据初始化
              </el-button>
            </div>
            <div class="buttonLeft" style="display: inline-block;margin-left:1vw;width: 11vw;margin-top: 8%;">
              <el-button style="font-size: 0.8vw;" @click="initChart">计算</el-button>
            </div>

            <div class="buttonRight" style="width: 11vw;display: inline-block;margin-top: 8%;">
              <el-button style="font-size: 0.8vw;margin-left: -1vw;" @click="clear">清除图片</el-button>
            </div>
            <div class="buttonLeft" style="display: inline-block;margin-left:1vw;width: 11vw;margin-top: 8%;">
              <el-button style="font-size: 0.8vw;" @click="save">保存</el-button>
            </div>

          </div>

        </div>
      </div>


      <div class="canshu">
        <div
            style="width: 100%;background-color: #004e9c;height: 2vw;border-radius: 0.6vw;text-align: center;color: #Ffffff;line-height: 2vw;font-size: 1vw;margin-top: 0.8%;">
          计算参数设置
        </div>
        <div style="display: flex;flex-direction: row;">
          <div style="width: 20%;height: 100%;">
            <div style="width: 100%;height: 3vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 7%;">
              <div style="width: 50%;line-height: 3vh;color: #Ffffff;font-size: 1vw;margin-left: 10%;">方位角(°)</div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.a" autocomplete="off"></el-input>
              </div>
            </div>
            <div style="width: 100%;height: 3vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 7%;">
              <div style="width: 50%;line-height: 3vh;color: #Ffffff;font-size: 1vw;margin-left: 10%;">发射仰角(rad)
              </div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.b_min" autocomplete="off"></el-input>
              </div>
            </div>
          </div>
          <div style="width: 20%;height: 100%;">
            <div style="width: 100%;height: 3vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 7%;">
              <div style="width: 50%;line-height: 3vh;color: #Ffffff;font-size: 1vw;margin-left: 10%;">发射射线数目
              </div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.Num" autocomplete="off"></el-input>
              </div>
            </div>
            <div style="width: 100%;height: 3vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 7%;">
              <div style="width: 14%;line-height: 3vh;color: #Ffffff;font-size: 1vw;">~</div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.b_max" autocomplete="off"></el-input>
              </div>
            </div>
          </div>
          <div style="width: 24%;height: 100%;">
            <div style="width: 100%;height: 3vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 6%;">
              <div style="width: 50%;line-height: 3vh;color: #Ffffff;font-size: 1vw;margin-left: 10%;">工作频率(MHz)
              </div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.fre" autocomplete="off"></el-input>
              </div>
            </div>
            <div style="width: 100%;height: 3vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 6%;">
              <div style="width: 50%;line-height: 3vh;color: #Ffffff;font-size: 1vw;margin-left: 10%;">
                F层底部高度(km)
              </div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.r_b" autocomplete="off"></el-input>
              </div>
            </div>
          </div>
          <div style="width: 30%;height: 100%;">
            <div style="width: 100%;height: 3vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 5%;">
              <div
                  style="width: 60%;line-height: 3vh;color: #Ffffff;font-size: 1vw;margin-left: 10%;white-space: nowrap;">
                电离层最大密度处的高度(km)
              </div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.r_m" autocomplete="off"></el-input>
              </div>
            </div>
            <div style="width: 100%;height: 3vh;margin-left: 3%;display: flex;flex-direction: row;margin-top: 5%;">
              <div style="width: 60%;line-height: 3vh;color: #Ffffff;font-size: 1vw;margin-left: 10%;">
                最大电子密度(10^12/m³)
              </div>
              <div class="inputbg" style="width: 30%;">
                <el-input v-model="form.N_m" autocomplete="off"></el-input>
              </div>
            </div>
          </div>
        </div>


      </div>

      <div class="loader" v-if="showJZ"></div>
      <!--          <div style="display: flex;flex-direction: column;">-->
      <!--            <div class="back4" style="margin-bottom: 2vh;">-->
      <!--              <div style="width: 35vw; height: 42vh;border-radius: 1vw;" v-if="src != ''">-->
      <!--                <el-image :src="src" @click="showBigInfo"-->
      <!--                  style="width: 100%; height: 42vh; margin-bottom: 1vh;border-radius: 1vw;"></el-image>-->
      <!--              </div>-->
      <!--            </div>-->
      <!--            <div style="margin-left: 45%;">-->
      <!--              <div slot="foot" class="dialog-footer">-->
      <!--                <el-button type="primary" class="button1" @click="test">载入测试值</el-button>-->
      <!--                <el-button type="primary" class="button1" @click="clear">清除</el-button>-->
      <!--                &lt;!&ndash; <el-button type="primary" class="button1" @click="save">保存</el-button> &ndash;&gt;-->
      <!--                <el-button type="primary" class="button1" @click="submitForm">计算</el-button>-->
      <!--              </div>-->
      <!--            </div>-->
      <!--          </div>-->
      <!--        </div>-->
      <!--      </div>-->
    </div>
    <el-dialog title="预览" :visible.sync="showBig">
      <div style="height: 28vw;width: 100%;margin: auto;display: flex;justify-content: center;" class="imgContainer"
           @wheel.prevent="handleWheel">
        <img :src="src" style="height: 100%;object-fit: contain;" :style="{ transform: `scale(${scale})` }"
             class="showBig">
      </div>

    </el-dialog>
  </div>
</template>

<script>

import * as echarts from 'echarts'
import html2canvas from "html2canvas";
import {fileUpdate} from "@/api/file";
import {saveJsResult} from "@/api/baogao";

export default {
  props: {
    jsId: {
      type: Number, // 根据实际类型调整
      required: true,         // 如果必传则设为 true
      default: null           // 默认值（可选）
    }
  },
  data() {
    return {
      showBig: false,
      loading: false,
      isVisible: true,
      src: "",
      urls: [],
      scale: 1,
      showJZ: false,
      dataFinal2: {
        jsId: null,
        jsResult: {},
        allImg: "",
      },
      form1: {},
      form: {
        a: 0,           // 方位角
        b_min: 0,         // 发射仰角
        Num: 0,         // 发射点经度
        b_max: 0,          // 发射点纬度
        fre: 0,       // 工作频率
        N_m: 0,  // 最大电子密度
        r_m: 0,       // 电离层最大高度
        r_b: 0     // 电离层底部高度
      }
    };
  },
  methods: {
    async initChart() {
      await this.$nextTick()
      const chart = echarts.init(document.getElementById('chart-container'));
      const res = await this.submitForm();

      const data = res.data;

      const results = []
      for (let i = 0; i < data.length; i++) {
        var points = [];
        let xPoint = data[i][0]
        console.log(xPoint.length)
        let yPoint = data[i][1]
        for (let j = 0; j < xPoint.length; j++) {
          let point = [xPoint[j], yPoint[j]]
          points.push(point)
        }
        results.push(points)
      }
      console.log()


      const series = results.map((points, index) => ({
        name: (res.data[0][2][index]).toFixed(2) + "",      // 系列名称（可自定义）
        type: 'line',                     // 图表类型（折线图）
        data: points,                     // 直接使用你的坐标集合
        smooth: true,                     // 平滑曲线
        symbol: 'none',                   // 不显示数据点标记
        lineStyle: {width: 2}           // 线宽
      }));

      // for(let a = 0;a<series.length;a++){
      //   series[a].name = res.data[1][3][a];
      // }

      console.log(series)
      // 4. 图表配置生成器
      const option = {

        tooltip: {
          trigger: 'axis'
        },
        // legend: {
        //   data: seriesData.map(item => item.name) // 从系列数据生成图例
        // },
        xAxis: {
          type: 'value',
          min: 0,
          max: 1000,
          name: '传播距离 (km)'
        },
        yAxis: {
          type: 'value',
          min: 0,
          max: 500,
          name: '射线高度 (km)'
        },
        series: series // 使用处理后的数据
      };

      chart.setOption(option);

    },
    showBigInfo() {
      this.showBig = true;
    },
    test() {
      this.form.a = 0;
      this.form.b_min = 0.1;
      this.form.b_max = 0.5;
      this.form.Num = 20;
      this.form.fre = 2.5;
      this.form.N_m = 1.1;
      this.form.r_m = 310;
      this.form.r_b = 109;
    },
    dataInitialize() {
      this.form.a = this.form1.a;
      this.form.b_min = this.form1.b_min;
      this.form.b_max = this.form1.b_max;
      this.form.Num = this.form1.Num;
      this.form.fre = this.form1.fre;
      this.form.N_m = this.form1.N_m;
      this.form.r_m = this.form1.r_m;
      this.form.r_b = this.form1.r_b;
    },
    async saveImage() {
      await this.$nextTick();
      const targetDiv = document.getElementById('capture');

      // 1. 先获取图表截图
      const chart = echarts.getInstanceByDom(document.getElementById('chart-container'));
      let chartImageUrl = '';
      if (chart) {
        chartImageUrl = chart.getDataURL({
          type: 'png',
          pixelRatio: 2,
          backgroundColor: '#fff'
        });
      }

      // 2. 克隆目标元素
      const clone = targetDiv.cloneNode(true);
      clone.style.position = 'absolute';
      clone.style.left = '-9999px';
      clone.style.whiteSpace = 'pre-wrap';
      clone.style.fontFamily = 'Arial, sans-serif';
      clone.style.fontSize = '1vw';

      // 3. 如果获取到了图表截图，替换克隆元素中的图表容器
      if (chartImageUrl) {
        const chartContainer = clone.querySelector('#chart-container');
        if (chartContainer) {
          // 清空图表容器并添加图片
          chartContainer.innerHTML = '';
          const img = document.createElement('img');
          img.src = chartImageUrl;
          img.style.width = '100%';
          img.style.height = '100%';
          img.style.objectFit = 'contain';
          chartContainer.appendChild(img);
        }
      }

      // 4. 处理其他样式
      const scrollableElements = clone.querySelectorAll('*[style*="overflow"]');
      scrollableElements.forEach(el => {
        el.style.overflow = 'visible';
        el.style.height = 'auto';
      });

      document.body.appendChild(clone);
      await new Promise(resolve => setTimeout(resolve, 500));

      // 5. 截图
      const canvas = await html2canvas(clone, {
        width: clone.scrollWidth,
        height: clone.scrollHeight,
        scale: 2,
        letterRendering: true,
        useCORS: true,
        backgroundColor: 'rgba(49,73,163,0.94)'
      });

      var imageData = canvas.toDataURL('image/png');
      console.log(imageData);

      var dataa = this.handleCapture(imageData);
      console.log(dataa);
      document.body.removeChild(clone);
    },
    closeModal() {
      this.isVisible = false;
      this.loading = false;
    },
    increment(property) {
      this.form[property] += 1; // 增加 1
    },
    decrement(property) {
      if (this.form[property] > 0) {
        this.form[property] -= 1;
      }
    },
    clear() {
      this.form.a = 0;
      this.form.b_min = 0;
      this.form.b_max = 0;
      this.form.Num = 0;
      this.form.fre = 0;
      this.form.N_m = 0;
      this.form.r_m = 0;
      this.form.r_b = 0;
      this.src = "";
    },
    handleWheel(e) {
      // 计算缩放比例
      const delta = e.deltaY > 0 ? -0.1 : 0.1;
      this.scale += delta;

      // 限制缩放范围
      this.scale = Math.min(Math.max(0.5, this.scale), 3);
    },
    async submitForm() {
      console.log(this.showJZ)
      this.showJZ = true;
      console.log(this.showJZ)
      this.loading = true
      // 处理表单提交
      var dataFinal1 = {
        a: this.form.a,           // 方位角
        b_min: this.form.b_min,// 发射仰角
        b_max: this.form.b_max,         // 发射点经度
        Num: this.form.Num,         // 发射点纬度
        fre: this.form.fre,       // 工作频率
        N_m: this.form.N_m,  // 最大电子密度
        r_m: this.form.r_m,     // 电离层最大高度
        r_b: this.form.r_b,  // 电离层底部高度
      }

      this.form1.a = dataFinal1.a;
      this.form1.b_min = dataFinal1.b_min;
      this.form1.b_max = dataFinal1.b_max;
      this.form1.Num = dataFinal1.Num;
      this.form1.fre = dataFinal1.fre;
      this.form1.N_m = dataFinal1.N_m;
      this.form1.r_m = dataFinal1.r_m;
      this.form1.r_b = dataFinal1.r_b;
      console.log(this.form1)
      const res = await this.$axios({
        url: "http://127.0.0.1:9080/dbdlc",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal1,
        headers: {
          'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      });
      this.showJZ = false
      return res;
      // .then((res) => {
      // this.urls.push(res.data);
      // this.$axios({
      //   // url:"http://192.168.220.1:9080/getpng?urls="+local,//请求的后台接口
      //   url: "http://127.0.0.1:10035/fileUpdate/getFile",//请求的后台接口
      //   method: "get",//get请求方式
      //   params: {urls: this.urls.join(",")},
      //   headers: {
      //     'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
      //     'Access-Control-Request-Method': 'GET',
      //     'Access-Control-Request-Headers': 'content-type',
      //   },
      // }).then((res) => {
      //   this.src = res.data.results[0].url;
      //   const combinedData = {
      //     ...dataFinal1,
      //     src: this.src,
      //   };
      // this.dataFinal2.jsResult = JSON.stringify(combinedData);

      // console.log(this.dataFinal2)
      // }).finally(() => {

      // })
      // })
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

      return new Blob([u8arr], {type: mime});
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
        this.dataFinal2.allImg = res.data.url;

        saveJsResult(this.dataFinal2).then((res) => {
          console.log(res);
        })


      })


    },
    async save() {
      this.dataFinal2.jsId = this.jsId;
      const combinedData = {
        ...this.form1,
      };
      this.dataFinal2.jsResult = JSON.stringify(combinedData);

      // 等待 ECharts 渲染完成
      await this.$nextTick();

      // 获取图表实例并确保渲染完成
      const chart = echarts.getInstanceByDom(document.getElementById('chart-container'));
      if (chart) {
        // 强制图表重绘
        chart.resize();
        await new Promise(resolve => setTimeout(resolve, 500)); // 等待渲染
      }

      this.saveImage();


      // this.$axios({
      //   url: "http://127.0.0.1:10035/save/JsResult",//请求的后台接口
      //   method: "post",//get请求方式
      //   data: this.dataFinal2,
      //   withCredentials: true, // 关键：允许发送 Cookie
      //   headers: {
      //     'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
      //     'Access-Control-Request-Method': 'POST',
      //     'Access-Control-Request-Headers': 'content-type',
      //   },
      // }).then((res) => {
      //   console.log(res)
      // })
    }
  }
};
</script>

<style scoped>
.content-container {
  width: 100%;
  height: 100%;
}


.background-container {
  padding: 0px;
  width: 98.5%;
  height: 95.2%;
  background-color: rgba(84, 195, 255, 0.45);
  /* 设置为视口高度 */
  background-size: cover;
  background-position: center;
  overflow: hidden;
  /* 隐藏超出背景图的内容 */
  margin-left: 0.5vw;
  margin-top: 1vh;
  border-radius: 1vw;
}

.showInfo {
  width: 96%;
  height: 12%;
  background-color: transparent;
  font-size: 0.9vw;
  margin-bottom: 2%;
  color: #FFFFFF;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  background-image: url('@/assets/img/back2.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
}

.showContent {
  width: 100%;
  height: 82%;
  background-color: transparent;
}

.showText {
  width: 96%;
  height: 35%;
  background-color: transparent;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  background-image: url('@/assets/img/back2.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
}

.comInfo {
  width: 100%;
  height: 20%;
  background-color: transparent;
  display: flex;
  /* justify-content: space-between; */
  align-items: center;
}

.Info1 {
  width: 45%;
  background-color: transparent;
  height: 100%;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  justify-items: center;
  align-items: center;
  margin-left: 2vw;
}

.yuan {
  width: 0.9vw;
  height: 0.9vw;
  background-color: aqua;
  border-radius: 50%;
  display: flex;
  justify-items: center;
}

.infoText {
  width: 60%;
  height: 100%;
  display: flex;
  align-items: center;
  background-color: transparent;
  margin-left: 1%;
}

.infoText input {
  height: 100%;
}

.text {
  width: 14vw;
  display: inline-block;
  color: #fff;
  white-space: nowrap;
  font-size: 0.8vw;
}

input {
  text-align: center;
  border: none;
  background-color: transparent;
  outline: none;
  color: #fff;
  width: 100%;
  font-size: 0.8vw;
}

.shuru {
  /* border: 1px solid aqua; */
  border-radius: 1vw;
  display: flex;
  justify-content: space-between;
  width: 8vw;
  background-image: url('@/assets/img/shurukuang.png');
  background-repeat: no-repeat;
  background-size: 98% 135%;
  background-position: 1%;
  height: 2.5vh;
}

.dialog-footer {
  float: right;
  /* margin-left: 80%; */
  display: flex;
}

.button1 {
  width: 4vw;
  border-radius: 2vw;
  line-height: 0vh;
  /*background-image: url('@/assets/img/queding.png');*/
  background-repeat: no-repeat;
  background-size: 100% 100%;
  display: flex;
  justify-content: center;
}

.buttons {
  display: flex;
  flex-direction: column;
  margin-right: 0.5vw;
}

.button2 {
  text-align: center;
  /*background-image: url('@/assets/img/zengjia.png');*/
  background-color: transparent;
  background-repeat: no-repeat;
  background-size: contain;
  height: 0.7vh;
  width: 0.5vw;
  border: none;
  margin-top: 0.4vh;
  margin-bottom: 0.2vh;
}

.button3 {
  text-align: center;
  /*background-image: url('@/assets/img/jianshao.png');*/
  background-color: transparent;
  background-repeat: no-repeat;
  background-size: contain;
  height: 0.8vh;
  width: 0.5vw;
  border: none;
}

.button4 {
  text-align: center;
  /*background-image: url('@/assets/img/zengjia.png');*/
  background-color: transparent;
  background-repeat: no-repeat;
  background-size: contain;
  height: 0.8vh;
  width: 0.5vw;
  border: none;
  margin-top: 0.4vh;
  margin-bottom: 0.2vh;
}

.button5 {
  text-align: center;
  /*background-image: url('@/assets/img/jianshao.png');*/
  background-color: transparent;
  background-repeat: no-repeat;
  background-size: contain;
  height: 0.7vh;
  width: 0.5vw;
  border: none;
}

.button6 {
  text-align: center;
  /*background-image: url('@/assets/img/jianshao.png');*/
  background-color: transparent;
  background-repeat: no-repeat;
  background-size: contain;
  height: 0.7vh;
  width: 0.5vw;
  border: none;
}

.button7 {
  text-align: center;
  background-color: transparent;
  background-repeat: no-repeat;
  background-size: contain;
  height: 0.8vh;
  width: 0.5vw;
  border: none;
}

/deep/ .el-image__error {
  width: 100%;
  height: 100%;
  background: transparent;
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
  padding-left: 1.5vw;
}

.back4 {
  background-image: url('@/assets/img/back4.png');
  background-size: 100% 100%;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
  width: 35vw;
  height: 42vh;
}

.back {
  background-image: url('@/assets/img/back.png');
  background-size: 100% 100%;
  width: 30vw;
  /* 拉伸图像以填充整个元素 */
  background-repeat: no-repeat;
}

.biaotou {
  background-image: url('@/assets/img/jianbianlv.png');
  height: 3vh;
}

.biaotouqian /deep/ .el-image__inner {
  height: 15%;
  width: 100%;
}

.formaction {
  height: 3vh;
  display: flex;
  justify-content: space-between;
  width: 28.5vw;
  padding-left: 3vw;
  margin-bottom: 0.5vh;
}

.formaction .el-input {
  display: flex;
  align-items: center;
  height: 100%;
}

.canshu /deep/ .el-input__inner {
  width: 100%;
  text-align: center;
  background-color: transparent;
  border: none;
  color: #fff;
}


.imgBox {
  background-color: #fff;
  border: #006cda 1px solid;
  width: 80%;
  height: 100%;
}

.canshu {
  background-color: #006cda;
  height: 20%;
  width: 94%;
  margin-left: 3%;
  margin-top: 2%;
}

.inputbg .el-input {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  width: 100%;
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

.showBig {
  max-width: 100%;
  max-height: 100%;
  transition: transform 0.1s ease;
}

.imgContainer {
  overflow: hidden;
}
</style>
