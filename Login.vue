<template>
  <div style="width: 100%;height: 100%;background-color: #00173a;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:99;" src="../assets/img/loginBg.png">
    <headLogin style="position: absolute;z-index: 100"></headLogin>
    <div class="loginBox" v-if="pageInfo=='login'">


      <div class="password-input-container">
        <div
            style="width: 100%;height: 1vw;position: relative;display: flex;flex-direction: row;justify-content: flex-start;margin-bottom: 0.5vw;">
          <img src="../assets/img/zcc.png" style="width: 1vw;height: 100%;">
          <div style="height:1vw;line-height: 1vw;color: white;font-size: 0.9vw;">用户名</div>
        </div>
        <img src="../assets/img/zcZh.png" style="position: absolute;z-index: 99;width: 100%;height: 100%;">
        <input
            type="text"
            placeholder="请输入用户名"
            v-model="userName"
        />
      </div>
      <div class="password-input-container1">
        <div
            style="width: 100%;height: 1vw;position: relative;display: flex;flex-direction: row;justify-content: flex-start;margin-bottom: 0.5vw;">
          <img src="../assets/img/zcc.png" style="width: 1vw;height: 100%;">
          <div style="height:1vw;line-height: 1vw;color: white;font-size: 0.9vw; ">密码</div>
        </div>
        <img src="../assets/img/zcPassword.png" style="position: absolute;z-index: 99;width: 100%;height: 100%;">
        <input
            type="text"
            :placeholder="placeholder2"
            v-model="password"
        />
      </div>
      <div class="checkBox">
        <el-checkbox style="color: rgba(255,255,255,0.68);position: absolute;right: 1vw;top: 0.5vw;" v-model="checked">
          记住密码
        </el-checkbox>
      </div>
      <div class="regist">
        <div style="float: left;margin-left: 42%;color: rgba(255,255,255,0.68);font-size: 0.8vw;">还没有账号，请进行
        </div>
        <div style="color: rgb(90,208,255);float: left;font-size: 0.8vw;" @click="openRest">注册</div>
      </div>


      <div class="loginButton" @click="login">
        <img src="../assets/img/loginButton.png" style="width: 100%;height: 100%;">
      </div>


      <img src="../assets/img/loginBox.png" style="width: 100%;height: 100%;">
    </div>


    <div class="zcBox" v-if="pageInfo=='zc'">

      <div class="password-zc-container">
        <div
            style="width: 100%;height: 1vw;position: relative;display: flex;flex-direction: row;justify-content: flex-start;margin-bottom: 0.5vw;">
          <img src="../assets/img/zcc.png" style="width: 1vw;height: 100%;">
          <div style="height:1vw;line-height: 1vw;color: white;font-size: 0.9vw; ">姓名</div>
        </div>
        <img src="../assets/img/zcName.png" style="position: absolute;z-index: 99;width: 100%;height: 100%;">
        <input
            type="text"
            placeholder="请输入姓名"
            v-model="form.useName"
        />
      </div>


      <div class="password-zc-container1">
        <div
            style="width: 100%;height: 1vw;position: relative;display: flex;flex-direction: row;justify-content: flex-start;margin-bottom: 0.5vw;">
          <img src="../assets/img/zcc.png" style="width: 1vw;height: 100%;">
          <div style="height:1vw;line-height: 1vw;color: white;font-size: 0.9vw; ">账号</div>
        </div>
        <img src="../assets/img/zcZh.png" style="position: absolute;z-index: 99;width: 100%;height: 100%;">
        <input
            type="text"
            placeholder="请输入账号"
            v-model="form.name"
        />
      </div>


      <div class="password-zc-container2">
        <div
            style="width: 100%;height: 1vw;position: relative;display: flex;flex-direction: row;justify-content: flex-start;margin-bottom: 0.5vw;">
          <img src="../assets/img/zcc.png" style="width: 1vw;height: 100%;">
          <div style="height:1vw;line-height: 1vw;color: white;font-size: 0.9vw; ">密码</div>
        </div>
        <img src="../assets/img/zcPassword.png" style="position: absolute;z-index: 99;width: 100%;height: 100%;">
        <input
            type="text"
            placeholder="请输入密码"
            v-model="form.password"
        />
      </div>

      <div class="password-zc-container3">
        <div
            style="width: 100%;height: 1vw;position: relative;display: flex;flex-direction: row;justify-content: flex-start;margin-bottom: 0.5vw;">
          <img src="../assets/img/zcc.png" style="width: 1vw;height: 100%;">
          <div style="height:1vw;line-height: 1vw;color: white;font-size: 0.9vw; ">用户类型</div>
        </div>
        <img src="../assets/img/zcType.png" style="position: absolute;z-index: 99;width: 100%;height: 100%;"
             v-if="typePic==0">
        <img src="../assets/img/zcTypeDown.png" style="position: absolute;z-index: 99;width: 100%;height: 100%;"
             v-if="typePic==1">

        <select v-model="form.userType" @click="changeType()">
          <option value="2" style="display:none; color:rgba(255, 255, 255, 0.54);" label="请选择用户类型"></option>
          <option label="管理员" value="1"></option>
          <option label="学生" value="0"></option>
        </select>
      </div>


      <div class="password-zc-container4">
        <div
            style="width: 100%;height: 1vw;position: relative;display: flex;flex-direction: row;justify-content: flex-start;margin-bottom: 0.5vw;">
          <img src="../assets/img/zcc.png" style="width: 1vw;height: 100%;">
          <div style="height:1vw;line-height: 1vw;color: white;font-size: 0.9vw; ">班级信息</div>
        </div>
        <img src="../assets/img/zcClass.png" style="position: absolute;z-index: 99;width: 100%;height: 100%;">
        <input
            type="text"
            placeholder="请输入班级信息"
            v-model="form.classInfo"
        />
      </div>

      <div class="zcButton" @click="goRegist">
        <div
            style="float: left;margin-left: 38%;color: rgba(255,255,255,0.68);margin-bottom: 0.5vw;text-decoration-line: underline;">
          已有账号，前往
        </div>
        <div style="color: rgb(90,208,255);float: left;text-decoration-line: underline;" @click="openLogin">登录</div>
        <img src="../assets/img/zcButton.png" style="width: 100%;height: 100%;">
      </div>
      <img src="../assets/img/zcBox.png" style="width: 100%;height: 100%;">
    </div>

  </div>

</template>
<script>

import headLogin from "@/components/HeadLogin.vue";
import {doLogin, registered} from "@/api/login";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Login',
  components: {headLogin},
  data() {
    return {
      placeholder1: "请输入账号",
      userName: "",
      placeholder2: "请输入密码",
      password: "",
      pageInfo: "login",
      checked: false,

      //这是注册的信息
      regist: false,
      form: {
        useName: "",
        name: '',
        password: '',
        userType: 2,
        classInfo: '',

      },
      formLabelWidth: '120px',
      typePic: 0,
    }
  },
  methods: {
    handleGlobalEnter(event) {
      const isEnter = event.key === 'Enter' || event.keyCode === 13;
      
      if (isEnter) {
        event.preventDefault(); // 阻止默认行为
        this.login();
      }
    },
    changeType() {
      if (this.typePic == 0) {
        this.typePic = 1;
      } else {
        this.typePic = 0
      }
    },
    login() {
      var data = {
        userName: this.userName,
        password: this.password,
      }
      doLogin(data).then((res) => {
        if (res.code == 200) {
          localStorage.setItem("type", res.info.userType)
          localStorage.setItem("name", res.info.userName)
          localStorage.setItem("uid", res.info.id)
          this.$router.push('/Mulu')
        } else {
          console.log(res.msg)
          this.$message.error(res.msg);
        }
      })
    },
    Check() {
      this.checked = true;
    },
    openRest() {
      this.pageInfo = "zc";
    },
    openLogin() {
      this.pageInfo = "login";
    },
    goRegist() {
      var data = {
        realName: this.form.useName,
        userName: this.form.name,
        password: this.form.password,
        userType: this.form.userType,
        classInfo: this.form.classInfo

      }
      registered(data).then((res) => {
        if (res.code == 200) {
          this.pageInfo = "login"
        }
        console.log(res);
      })
    }
  },
  mounted() {
    // this.login();
    window.addEventListener('keydown', this.handleGlobalEnter);
  },
  beforeDestroy() {
    window.removeEventListener('keydown', this.handleGlobalEnter);
  },
}
</script>
<style scoped>
.loginBox {
  width: 48%;
  height: 60%;
  //background-color: #42b983;
  position: absolute;
  z-index: 100;
  top: 15%;
  left: 40%;
}

.password-input-container {
  width: 70%;
  height: 8%;
  //background: #b94289;
  position: absolute;
  top: 29%;
  left: 19%;
}

.password-input-container1 {
  width: 70%;
  height: 8%;
  //background: #b94289;
  position: absolute;
  top: 49%;
  left: 19%;
}

input {
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
  color: white; /* 文字颜色 */
  background-color: transparent;
  padding-left: 3%;
  position: absolute;
  z-index: 2000;

}

input::placeholder {
  color: rgba(255, 255, 255, 0.54);
  opacity: 1; /* Firefox 默认将 placeholder 的透明度设置为 0.54 */

}

.checkBox {
  width: 80%;
  height: 5%;
  position: absolute;
  top: 61%;
  left: 10%;
}

/* 自定义样式 */
.el-checkbox__inner {
  background-color: transparent !important;
  border-color: transparent !important;
}

.el-checkbox__input.is-checked .el-checkbox__inner {
  background-color: transparent !important;
  border-color: transparent !important;
}

.el-checkbox__input.is-indeterminate .el-checkbox__inner {
  background-color: transparent !important;
  border-color: transparent !important;
}

.regist {
  width: 80%;
  height: 12%;
  position: absolute;
  bottom: 15%;
  left: 12%;
  color: #Ffffff;
  text-align: center;
}

/*登录按钮*/
.loginButton {
  width: 69%;
  height: 10%;
  position: absolute;
  bottom: 12%;
  left: 20%;

}


/*注册*/
.zcBox {
  width: 50%;
  height: 78%;
  //background-color: #42b983;
  position: absolute;
  z-index: 100;
  top: 12%;
  left: 39%;
}

.password-zc-container {
  width: 70%;
  height: 7%;
  //background: #b94289;
  position: absolute;
  top: 18.5%;
  left: 19%;
}

.password-zc-container1 {
  width: 70%;
  height: 6%;
  //background: #b94289;
  position: absolute;
  top: 30.5%;
  left: 19%;
}

.password-zc-container2 {
  width: 70%;
  height: 6%;
  //background: #b94289;
  position: absolute;
  top: 42.5%;
  left: 19%;
}

.password-zc-container3 {
  width: 70%;
  height: 6%;
  //background: #b94289;
  position: absolute;
  top: 54.5%;
  left: 19%;
}

.password-zc-container4 {
  width: 70%;
  height: 6%;
  //background: #b94289;
  position: absolute;
  top: 66.5%;
  left: 19%;
}

.zcButton {
  width: 68%;
  height: 8%;
  position: absolute;
  bottom: 12%;
  left: 20%;
}

select {
  //background-image: url("../assets/img/zcType.png");
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
  color: white; /* 文字颜色 */
  background-color: transparent;
  padding-left: 3%;
  position: absolute;
  z-index: 2000;
  appearance: none;
}

option {
  color: black;
  background: rgb(255, 255, 255);
  line-height: 20px;
}

option:hover {
  background: #EBCCD1;
}

</style>
