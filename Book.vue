<template>
  <div style="width: 100%;height: 100%;">
    <div style="width: 100%;height: 4vw;background-color: #42b983;">
      <div style="background-color: silver;width: 3vw;height: 2vw;line-height: 2vw;text-align: center;" @click="goHome">跳转回去</div>
    </div>
    <div>
      <el-button type="info" plain icon="el-icon-upload2" size="mini" @click="openFileInput">导入</el-button>

      <input
          ref="fileInput"
          type="file"
          accept=".doc, .docx"
          style="display: none;"
          @change="handleFileChange"
      />
    </div>
    <div>


      aaaaaaaaaaaaaaaaaaa{{num}}

    </div>
    <el-button type="primary" @click="goToCalculator">跳转到Calculator</el-button>
    <div>
    <el-button @click="dialogVisible = true">点击打开弹窗</el-button>
    <el-dialog :visible.sync="dialogVisible" title="提示">
      <p>这是一个简单的内容。</p>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
    </div>
<!--    <div style="width: 100%;height: 100%;">-->
<!--      <div class="gContainer">-->
<!--        <div id="graph-panel" style="width: 100%;height: 100%;"></div>-->
<!--      </div>-->
<!--    </div>-->
  </div>

</template>
<script>
import {getgraphInfo} from "@/api/login";
import {addFile} from "@/api/file";
import VisGraph from '@/assets/js/graphvis.min.20241008.js'
import LayoutFactory from '@/assets/js/graphvis.layout.min.js'
import {config} from '@/assets/defaultConfig.js'
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Home',
  data() {
    return{
      dialogVisible: false,
      num:undefined,
      infos:[],
      demoData:{},
      graphData: {
        nodes: [],
        links: []
      },
      config,
    }
  },
  methods:{

    openFileInput() {
      // 触发隐藏的文件输入框点击事件
      this.$refs.fileInput.click();
    },
    handleFileChange(event) {
      const file = event.target.files[0];
      if (file) {
        this.uploadFile(file);
      }
    },
    uploadFile(file) {
      // 调用API函数进行文件上传
      addFile(file)
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
            this.$refs.fileInput.value = null;
          });
    },

    goHome(){
      this.$router.push('/Graph')
    },
    goToCalculator() {
      this.$router.push('/Calculator')
    },
    onCreated(editor) {
      this.editor = Object.seal(editor) // 一定要用 Object.seal() ，否则会报错
    },
    getInfo(){
      var data = {}
      getgraphInfo(data).then((res)=>{
        console.log(res);
        this.infos = res;
        var data1 = {};
        data1.nodes = this.infos.docList;
        data1.links = this.infos.relaList;
        this.zhengl(data1)

      })
    },
    async drawGraphData() {
      this.graphData = this.demoData;
      if (this.visGraph === null) {
        this.createGraph();
        // this.genrateGraphData();
        this.visGraph.drawData(this.graphData);
        // this.refreshGraphData();
        this.visGraph.incremaNodesCodinate(this.graphData.nodes);
        this.reLayout();
        // this.goCenter();
      } else {
        this.createGraph();

        this.visGraph.drawData(this.graphData);
        // this.refreshGraphData();
        this.visGraph.incremaNodesCodinate(this.graphData.nodes);
        this.reLayout();
        // this.goCenter();
      }
      this.loading = false;
    },
    // 创建全局绘图客户端对象
    createGraph() {
      this.visGraph = new VisGraph(document.getElementById('graph-panel'), this.config)
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
    zhengl(data) {
      const nodes = []
      const links = [] // 存放节点和关系
      // const nodeSet = [] // 存放去重后nodes的id
      var nodeList = data.nodes;
      var lineList = data.links;
      console.log(nodeList);
      console.log(lineList);
      for (let a = 0; a < nodeList.length; a++) {
        if (nodeList[a].group == '0') {
          const aaa = {name: nodeList[a].docTitle, docId: nodeList[a].docId,docLevel: nodeList[a].group}
          nodes.push({
            id: nodeList[a].Id,
            label: nodeList[a].docTitle,
            properties: aaa,
            size: 450,
            color: '227,203,0',
            font: 'normal 70px Arial',
            fontColor: '255,255,255'
          })
        }
        if (nodeList[a].group == '1') {
          const aaa = {name: nodeList[a].docTitle, docId: nodeList[a].docId,docLevel: nodeList[a].group}
          nodes.push({
            id: nodeList[a].Id,
            label: nodeList[a].docTitle,
            properties: aaa,
            size: 350,
            width:350,
            height:300,
            color: '47,47,230',
            font: 'normal 68px Arial',
            fontColor: '255,255,255'
          })
        }
        if (nodeList[a].group == '2') {
          const aaa = {name: nodeList[a].docTitle, docId: nodeList[a].docId,docLevel: nodeList[a].group}
          nodes.push({
            id: nodeList[a].Id,
            label: nodeList[a].docTitle,
            properties: aaa,
            size: 300,
            width:300,
            height:250,
            color: '255,138,0',
            font: 'normal 50px Arial',
            fontColor: '255,255,255'
          })
        }
        if (nodeList[a].group == '3') {
          const aaa = {name: nodeList[a].docTitle, docId: nodeList[a].docId,docLevel: nodeList[a].group}
          nodes.push({
            id: nodeList[a].Id,
            label: nodeList[a].docTitle,
            properties: aaa,
            size: 250,
            width:250,
            height:250,
            color: '30,255,0',
            font: 'normal 40px Arial',
            fontColor: '0,0,0'
          })
        }
        if (nodeList[a].group == '4') {
          const aaa = {name: nodeList[a].docTitle, docId: nodeList[a].docId,docLevel: nodeList[a].group}
          nodes.push({
            id: nodeList[a].Id,
            label: nodeList[a].docTitle,
            properties: aaa,
            size: 200,
            width:200,
            height:200,
            color: '248,143,248',
            font: 'normal 32px Arial',
            fontColor: '255,255,255'
          })
        }
        if (nodeList[a].group == '5') {
          const aaa = {name: nodeList[a].docTitle, docId: nodeList[a].docId,docLevel: nodeList[a].group}
          nodes.push({
            id: nodeList[a].Id,
            label: nodeList[a].docTitle,
            properties: aaa,
            size: 150,
            width:150,
            height:150,
            color: '65,154,255',
            font: 'normal 30px Arial',
            fontColor: '255,255,255'
          })
        }
        if (nodeList[a].group == '6') {
          const aaa = {name: nodeList[a].docTitle, docId: nodeList[a].docId,docLevel: nodeList[a].group}
          nodes.push({
            id: nodeList[a].Id,
            label: nodeList[a].docTitle,
            properties: aaa,
            size: 100,
            width:100,
            height:100,
            color: '0,228,255',
            font: 'normal 28px Arial',
            fontColor: '0,0,0'
          })
        }

      }


      for (let b = 0; b < lineList.length; b++) {

        var bbb = {name: lineList[b].relate}
        links.push({
          source: lineList[b].source,
          target: lineList[b].target,
          type: lineList[b].relate,
          properties: bbb,
          color: '202,202,202',
          lineWidth: 3,
        })
      }

      this.demoData = {
        "nodes": nodes,
        "links": links
      }
      this.drawGraphData();
    }
  },
  mounted() {
    // this.getInfo();
    this.num = this.$route.query.id;
  }
}
</script>
<style scoped>
.gContainer {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  width: 100%;
  height: 45vw;
}
</style>
