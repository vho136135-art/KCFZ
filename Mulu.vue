<template>
  <div style="width: 100%;height: 100%;">
    <img style="width: 100%;height: 100%;position: absolute;z-index:99;" src="../assets/img/mulubg.png">
    <headInfo style="position: absolute;z-index: 100"></headInfo>
    <div class="mululist">
      <div v-for="item in mulu" :key="item" style="width: 100%;height: 10%;" @click="goPage(item.info)">
        <img v-if="item.name == '图文认知' && muluName != '图文认知'" :src="item.url" style="width: 10vw;height: 12.5vw;margin-top: 2.3vw;"
          @mouseenter="changeInfo(item.name)">
        <img v-if="item.name == '图文认知' && muluName == '图文认知'" :src="item.urlChoose"
             style="width: 15vw;height: 17.5vw;margin-top: -0.5vw;">

        <img v-if="item.name == '视频资源' && muluName != '视频资源'" :src="item.url"
             style="width: 10vw;height: 12.5vw;margin-top: 2.3vw;" @mouseenter="changeInfo(item.name)">
        <img v-if="item.name == '视频资源' && muluName == '视频资源'" :src="item.urlChoose"
             style="width: 15vw;height: 17.5vw;margin-top: -0.5vw;">


        <img v-if="item.name == '动画显示' && muluName != '动画显示'" :src="item.url"
          style="width: 10vw;height: 12.5vw;margin-top: 2.3vw;" @mouseenter="changeInfo(item.name)">
        <img v-if="item.name == '动画显示' && muluName == '动画显示'" :src="item.urlChoose"
          style="width: 15vw;height: 17.5vw;margin-top: -0.5vw;">

        <img v-if="item.name == '数值计算' && muluName != '数值计算'" :src="item.url"
             style="width: 11vw;height: 14vw;margin-top: 1.5vw;" @mouseenter="changeInfo(item.name)">
        <img v-if="item.name == '数值计算' && muluName == '数值计算'" :src="item.urlChoose"
             style="width: 16vw;height: 19vw;margin-top: -1.5vw;">

        <img v-if="item.name == '知识图谱' && muluName != '知识图谱'" :src="item.url"
             style="width: 12vw;height: 17vw;" @mouseenter="changeInfo(item.name)">
        <img v-if="item.name == '知识图谱' && muluName == '知识图谱'" :src="item.urlChoose"
             style="width: 17vw;height: 22vw;margin-top: -3vw;">


        <img v-if="item.name == '辅助决策' && muluName != '辅助决策'" :src="item.url"
          style="width: 11vw;height: 14vw;margin-top: 1.5vw;" @mouseenter="changeInfo(item.name)">
        <img v-if="item.name == '辅助决策' && muluName == '辅助决策'" :src="item.urlChoose"
          style="width: 16vw;height: 19vw;margin-top: -1.5vw;">

        <img v-if="item.name == '帮助文档' && muluName != '帮助文档'" :src="item.url" style="width: 12vw;height: 17vw;"
          @mouseenter="changeInfo(item.name)">
        <img v-if="item.name == '帮助文档' && muluName == '帮助文档'" :src="item.urlChoose"
          style="width: 17vw;height: 22vw;margin-top: -3vw;">
      </div>
    </div>

    <div style="width: 100%;height: 3%;position: fixed;bottom: 0px;z-index: 100">
      <foot></foot>
    </div>
  </div>

</template>
<script>

import headInfo from "@/components/HeadMulu.vue";
import Foot from "@/components/Foot.vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Home',
  components: { Foot, headInfo },
  data() {
    return {
      muluName: "",
      mulu: [
        { id: 0, name: "知识图谱", info: "Graph", url: require("../assets/img/nleft1.png"), urlChoose: require("../assets/img/nleft12.png") },
        { id: 1, name: "辅助决策", info: "BaoGao", url: require("../assets/img/nleft2.png"), urlChoose: require("../assets/img/nleft22.png") },
        { id: 2, name: "图文认知", info: "TwInfo", url: require("../assets/img/nleft3.png"), urlChoose: require("../assets/img/nleft32.png") },
        { id: 3, name: "视频资源", info: "SpInfo", url: require("../assets/img/nleft4.png"), urlChoose: require("../assets/img/nleft42.png") },
        { id: 4, name: "动画显示", info: "DhInfo", url: require("../assets/img/nleft5.png"), urlChoose: require("../assets/img/nleft52.png") },
        { id: 5, name: "数值计算", info: "JsInfo", url: require("../assets/img/nleft6.png"), urlChoose: require("../assets/img/nleft62.png") },
        { id: 6, name: "帮助文档", info: "HelpInfo", url: require("../assets/img/left7.png"), urlChoose: require("../assets/img/left72.png") },
      ]
      //  {id:4,name:"知识图谱",info:"Graph",url:require("../assets/img/left5.png"),urlChoose:require("../assets/img/left52.png")},
      //  {id:5,name:"辅助决策",info:"BaoGao",url:require("../assets/img/left6.png"),urlChoose:require("../assets/img/left62.png")},



    }
  },
  methods: {
    changeInfo(name) {
      this.muluName = name;
    },
    goPage(info) {
      if (info == "TwInfo") {
        localStorage.setItem("pageNum", 1)
      }
      this.$router.push('/' + info)

    }

  },
  mounted() {

  }
}
</script>
<style scoped>
.mululist {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  width: 94%;
  height: 50%;
  position: absolute;
  top: 33%;
  z-index: 110;
  left: 3%;
  text-align: center;
  font-size: 1.2vw;
  color: #ffffff;
}
</style>
