<template>
  <div class="background-container">
    <div class="content-container" id="capture">
      <div
          style="display: flex;width: 100%;margin-bottom: 1vh;margin-top: 2vh;align-items: center;justify-items: center;justify-content: center;">
        <div style="color: #004e9c; font-size: 1.6vw;font-weight: 500;">
          面向舰机超短波通信的表面波导可用性评估软件
        </div>


        <!--        <el-button type="primary" class="button1" style="height: 1.5vw;margin-left: 33vw;" @click="save">保存</el-button>-->
      </div>
      <img style="height: 0.15vw;object-fit: contain;" src="@/assets/img/hengxian.png">
      <div style="width: 40%;height: 70%;background-color: #006cda;margin-top: 2%;margin-left: 30%;padding-top: 0.3vh">
        <div style="display: flex;width: 31vw;margin-bottom: 1vh;margin-left: 1vw;margin-top: 0.3vw;" class="biaotou">
          <div style="vertical-align: middle;align-items: center;position: relative;">
            <el-image :src="require('@/assets/img/qianbiao.png')"  style="display: inline-block;height: 100%;" />
            <div style="color: #fff; white-space: nowrap;font-size: 0.9vw;position: absolute;
              top: 0;display: flex;justify-content: left;justify-items: center;align-items: center;left: 0.5vw;">
              <div style="height: 0.4vw;width: 0.6vw;border-radius: 2vw;background-color: #FFFFFF;margin-left: 0.1vw;margin-right: 0.2vw;"></div>
              <div >参数设置</div>
            </div>


          </div>
        </div>
        <div style="width: 94%;height: 2.5vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;align-items: center;">
          <div style="width: 50%;line-height: 2.5vw;color: #Ffffff;font-size: 1vw;margin-left: 10%;">飞机高度H(m)</div>
          <div class="inputbg" style="width: 30%;">
            <el-input v-model="form.H" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
          </div>
        </div>
        <div style="width: 94%;height: 2.5vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;align-items: center;">
          <div style="width: 50%;line-height: 2.5vw;color: #Ffffff;font-size: 1vw;margin-left: 10%;">表面波导厚度D(m)</div>
          <div class="inputbg" style="width: 30%;">
            <el-input v-model="form.D" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
          </div>
        </div>
        <div style="width: 94%;height: 2.5vw;margin-left: 3%;display: flex;flex-direction: row;margin-top: 2%;align-items: center;">
          <div style="width: 50%;line-height: 2.5vw;color: #Ffffff;font-size: 1vw;margin-left: 10%;">超短波频率F(mHz)</div>
          <div class="inputbg" style="width: 30%;">
            <el-input v-model="form.F" autocomplete="off" @focus="onFocus" @blur="onBlur"></el-input>
          </div>
        </div>



        <div style="display: flex;width: 31vw;margin-bottom: 1vh;margin-left: 1vw;margin-top: 0.3vw;" class="biaotou">
          <div style="vertical-align: middle;align-items: center;position: relative;">
            <el-image :src="require('@/assets/img/qianbiao.png')"  style="display: inline-block;height: 100%;" />
            <div style="color: #fff; white-space: nowrap;font-size: 0.9vw;position: absolute;
              top: 0;display: flex;justify-content: left;justify-items: center;align-items: center;left: 0.5vw;">
              <div style="height: 0.4vw;width: 0.6vw;border-radius: 2vw;background-color: #FFFFFF;margin-left: 0.1vw;margin-right: 0.2vw;"></div>
              <div >操作</div>
            </div>


          </div>
        </div>

        <div style="width: 100%;height: 6vw;display: flex;flex-direction: row;justify-content: space-around;justify-items: center;align-items: center;margin-left: 3vw;margin-top: 0.6vw;">
          <div style="width: 48%;height: 100%;">
            <div style="width: 10vw;height: 3vw;text-align: center;padding-left: 2vw;font-size: 1vw;line-height: 2vw;color: #FFFFFF;" class="buttonLeft" @click="test">
              载入测试值
            </div>
            <div style="width: 10vw;height: 3vw;text-align: center;padding-left: 2vw;font-size: 1vw;line-height: 2vw;color: #FFFFFF;" class="buttonLeft" @click="clear">
              清除数据
            </div>
          </div>
          <div style="width: 48%;height: 100%">
            <div style="width: 10vw;height: 3vw;text-align: center;padding-right:2vw;font-size: 1vw;line-height: 2vw;color: #FFFFFF;" class="buttonRight" @click="submitForm">
              计算
            </div>

            <div style="width: 10vw;height: 3vw;text-align: center;padding-right: 2vw;font-size: 1vw;line-height: 2vw;color: #FFFFFF;" class="buttonRight" @click="save">
              保存
            </div>
          </div>


        </div>

        <div style="display: flex;width: 31vw;margin-bottom: 1vh;margin-left: 1vw;margin-top: 0.3vw;" class="biaotou">
          <div style="vertical-align: middle;align-items: center;position: relative;">
            <el-image :src="require('@/assets/img/qianbiao.png')"  style="display: inline-block;height: 100%;" />
            <div style="color: #fff; white-space: nowrap;font-size: 0.9vw;position: absolute;
              top: 0;display: flex;justify-content: left;justify-items: center;align-items: center;left: 0.5vw;">
              <div style="height: 0.4vw;width: 0.6vw;border-radius: 2vw;background-color: #FFFFFF;margin-left: 0.1vw;margin-right: 0.2vw;"></div>
              <div >结果显示</div>
            </div>


          </div>
        </div>

        <div style="font-size: 1.5vw;color: #Ffffff;width: 100%;display: flex;justify-content: center;margin-top: 2%;">{{answer}}</div>






      </div>


    </div>

  </div>
</template>

<script>




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
      answer:"",
      showBig:false,
      loading: false,
      isVisible: true,
      src: "",
      urls: [],
      showJZ: false,
      dataFinal3:{
        H: 0,           // 方位角
        D: 0,         // 发射仰角
        F: 0,
        answer:""
      },
      dataFinal2: {
        jsId: null,
        jsResult: {},
        allImg: "",
      },
      form: {
        H: 0,           // 方位角
        D: 0,         // 发射仰角
        F: 0,
      }
    };
  },
  methods: {
    test(){
      this.form.H = 16;
      this.form.D = 100;
      this.form.F = 125;
    },


    closeModal() {
      this.isVisible = false;
      this.loading = false;
    },

    clear() {
      this.form.H = 0;
      this.form.D = 0;
      this.form.F = 0;
    },
    submitForm() {
      console.log(this.showJZ)
      this.showJZ = true;
      console.log(this.showJZ)
      this.loading = true
      // 处理表单提交
      var dataFinal1 = {
        H: this.form.H,           // 方位角
        D: this.form.D,// 发射仰角
        F: this.form.F,         // 发射点经度
      }

      this.$axios({
        url: "http://127.0.0.1:9080/cdbtx",//请求的后台接口
        method: "post",//get请求方式
        data: dataFinal1,
        headers: {
          'Origin': 'http://127.0.0.1:8080', // 你的前端应用的源
          'Access-Control-Request-Method': 'POST',
          'Access-Control-Request-Headers': 'content-type',
        },
      }).then((res) => {
        console.log(res)
        this.showJZ = false
        this.answer = res.data;
      })
    },


    save() {
      this.dataFinal2.jsId = this.jsId;
      this.dataFinal3.H = this.form.H;
      this.dataFinal3.D = this.form.D;
      this.dataFinal3.F = this.form.F
      this.dataFinal3.answer = this.answer
      this.dataFinal2.jsResult = JSON.stringify(this.dataFinal3)
      this.$axios({
        url: "http://127.0.0.1:10035/save/JsResult",//请求的后台接口
        method: "post",//get请求方式
        data: this.dataFinal2,
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
  width: 5vw;
  border-radius: 2vw;
  line-height: 0vh;
  /*background-image: url('@/assets/img/queding.png');*/
  background-repeat: no-repeat;
  background-size: 100% 100%;
  text-align: center;
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
  background-color: #006cda;
  width: 30vw;
  /* 拉伸图像以填充整个元素 */

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

.formaction /deep/ .el-input__inner {
  width: 100%;
  text-align: center;
  background-color: transparent;
  border: none;
  color: #fff;
}

.inputbg .el-input {
  background-image: url('@/assets/img/graphInputNew.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  width: 100%;
  height: 2vw;
}
/deep/ .el-input__inner {
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
</style>
