<template>
  <div>
    <div style="height:calc(100vh);">
      <RelationGraph ref="graphRef" :options="graphOptions" :on-node-expand="onNodeExpand" :on-line-collapse="onNodeCollapse">
      </RelationGraph>
    </div>
  </div>
</template>

<script>
import { getgraphInfo } from "@/api/login";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Graph',
  components: {},
  data() {
    return {
      openLevel: 7,
      demoData: {},
      graphOptions: {
        debug: false,
        lineUseTextPath: true,
        layout: {
          label: '树',
          layoutName: 'tree',
          layoutClassName: 'seeks-layout-center',
          from: 'top',
          // 通过这4个属性来调整 tree-层级距离&节点距离

          levelDistance: 200,      // 层与层之间的垂直间距
          nodeDistance: 150,       // 同一层级的水平间距
          min_per_width: 120,      // 最小水平间距（固定值）
          max_per_width: 120,      // 最大水平间距（固定值，强制均匀分布）
          min_per_height: 300,     // 最小垂直间距（固定值）
          max_per_height: 300,     // 最大垂直间距（固定值，强制对齐）
          disableDrag: true,       // 禁止拖动节点（可选）
          align: 'center',         // 居中排列
          fixed: false,            // 允许自动布局调整
        },
        lineWidth: 0.2,
        defaultLineWidth: 2,
        defaultLineShape: 1,
        defaultNodeShape:0,
        defaultNodeBorderWidth: 0,
        defaultLineColor: 'rgba(0, 186, 189, 1)',
        defaultNodeColor: 'rgba(0, 206, 209, 1)',
        lineLengths:100,

      }
    }
  },
  methods: {

    async openByLevel() {
      const graphInstance = this.$refs.graphRef.getInstance();
      // // 重置数据
      graphInstance.getNodes().forEach(node => {
        node.expanded = true;
      });
      // graphInstance.getNodes().forEach(node => {
      //   console.log(node)
      //   console.log(node.text);
      //   // 判断节点的级别（根节点为0）
      //
      // })
      await graphInstance.doLayout();
    },
    onNodeCollapse(node) {
      // 折叠节点时，只隐藏其下层节点
      const graphInstance = this.$refs.graphRef.getInstance();
      const allNodes = graphInstance.getNodes();

      // 1. 找到所有子节点
      const childNodes = allNodes.filter(n => {
        return this.demoData.lines.some(line =>
            line.from === node.id && line.to === n.id
        );
      });

      // 2. 只隐藏子节点（不隐藏父节点）
      childNodes.forEach(child => {
        child.expanded = false;
        child.hide = true; // 可能需要根据RelationGraph的具体API调整
      });

      graphInstance.doLayout();
    },
    showGraph() {
      let params = {};
      getgraphInfo(params).then((res) => {
        this.zhengl(res.data);
        this.$refs.graphRef.setJsonData(this.demoData, () => {
          this.openByLevel(this.openLevel);
        });
      })
    },
    zhengl(data) {
      const nodes = []
      const lines = [] // 存放节点和关系
      var nodeList = data.nodes;
      var lineList = data.links;
      console.log(data)
      if (nodeList != undefined) {
        var leve0Nodes = nodeList.filter(node => node.group === '0' && node.type === 0);
        console.log(leve0Nodes);
        var startX = - (leve0Nodes.length * 150) / 2; // 居中起始位置
        leve0Nodes.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 0,
            x: startX + index * 150, // 水平等距排列
            y: 200,                 // leve0 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },
          });
        });
        var leve1Nodes = nodeList.filter(node => node.group === '1' && node.type === 0);
        var startX1 = - (leve1Nodes.length * 150) / 2; // 居中起始位置
        leve1Nodes.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startX1 + index * 150, // 水平等距排列
            y: 400,                 // leve1 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },
          });
        });
        var leve2Nodes = nodeList.filter(node => node.group === '2' && node.type === 0);
        var startX2 = - (leve2Nodes.length * 150) / 2; // 居中起始位置
        leve2Nodes.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 2,
            x: startX2 + index * 150, // 水平等距排列
            y: 600,                 // leve2 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },
          });
        });
        var leve3Nodes = nodeList.filter(node => node.group === '3' && node.type === 0);
        var startX3 = - (leve3Nodes.length * 150) / 2; // 居中起始位置
        leve3Nodes.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 3,
            x: startX3 + index * 150, // 水平等距排列
            y: 800,                 // leve3 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },
          });
        });
        var leve4Nodes = nodeList.filter(node => node.group === '4' && node.type === 0);
        var startX4 = - (leve4Nodes.length * 150) / 2; // 居中起始位置
        leve4Nodes.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 4,
            x: startX4 + index * 150, // 水平等距排列
            y: 1000,                 // leve4 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },
          });
        });
        var leve5Nodes = nodeList.filter(node => node.group === '5' && node.type === 0);
        // console.log(leve5Nodes)
        var startX5 = - (leve5Nodes.length * 150) / 2; // 居中起始位置
        leve5Nodes.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 5,
            x: startX5 + index * 150, // 水平等距排列
            y: 1200,                 // leve5 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },
          });
        });
        var leve6Nodes = nodeList.filter(node => node.group === '6' && node.type === 0);
        // console.log(leve6Nodes)
        var startX6 = - (leve6Nodes.length * 150) / 2; // 居中起始位置
        leve6Nodes.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 6,
            x: startX6 + index * 150, // 水平等距排列
            y: 1400,                 // leve6 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },
          });
        });
        var leve7Nodes = nodeList.filter(node => node.group === '7' && node.type === 0);
        console.log(leve7Nodes)
        var startX7 = - (leve7Nodes.length * 150) / 2; // 居中起始位置
        leve7Nodes.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 7,
            x: startX7 + index * 150, // 水平等距排列
            y: 1600,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },

            expandHolderPosition: 'bottom',
          });
        });


        var NodesText1 = nodeList.filter(node => node.group === '1' && node.type !== 0);
        console.log(NodesText1)
        var startText1 = - (NodesText1.length * 150) / 2; // 居中起始位置
        NodesText1.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText1 + index * 150, // 水平等距排列
            y: 1800,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },

            expandHolderPosition: 'bottom',
          });
        });
        var NodesText2 = nodeList.filter(node => node.group === '2' && node.type !== 0);
        console.log(NodesText2)
        var startText2 = - (NodesText2.length * 150) / 2; // 居中起始位置
        NodesText2.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText2 + index * 150, // 水平等距排列
            y: 2000,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },

            expandHolderPosition: 'bottom',
          });
        });
        var NodesText3 = nodeList.filter(node => node.group === '3' && node.type !== 0);
        console.log(NodesText3)
        var startText3 = - (NodesText3.length * 150) / 2; // 居中起始位置
        NodesText3.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText3 + index * 150, // 水平等距排列
            y: 2200,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },

            expandHolderPosition: 'bottom',
          });
        });
        var NodesText4 = nodeList.filter(node => node.group === '4' && node.type !== 0);
        console.log(NodesText4)
        var startText4 = - (NodesText4.length * 150) / 2; // 居中起始位置
        NodesText4.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText4 + index * 150, // 水平等距排列
            y: 2400,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },

            expandHolderPosition: 'bottom',
          });
        });
        var NodesText5 = nodeList.filter(node => node.group === '5' && node.type !== 0);
        console.log(NodesText5)
        var startText5 = - (NodesText5.length * 150) / 2; // 居中起始位置
        NodesText5.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText5 + index * 150, // 水平等距排列
            y: 2600,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            properties: { ...node },

            expandHolderPosition: 'bottom',
          });
        });

        // for (let a = 0; a < nodeList.length; a++) {
        //   if(parseInt(nodeList[a].group)!=0){
        //     nodes.push({
        //       id: nodeList[a].id,
        //       text: nodeList[a].name,
        //       leve: parseInt(nodeList[a].group),
        //       properties: {
        //         name: nodeList[a].name,
        //         docId: nodeList[a].docId,
        //         parent: nodeList[a].parentId,
        //         leve: parseInt(nodeList[a].group),
        //         type: nodeList[a].type
        //       },
        //
        //     });
        //   }
        //
        // }
      }

      // var allOne = nodeList[0].docId

      if (lineList != undefined) {
        for (let b = 0; b < lineList.length; b++) {
          const sourceId = lineList[b].source;
          const targetId = lineList[b].target;

          // 检查 source 和 target 是否存在于节点的 id 中
          const sourceNodeExists = nodes.some(node => node.id === sourceId);
          const targetNodeExists = nodes.some(node => node.id === targetId);
          if (!sourceNodeExists) {
            console.error(`Source node with id ${sourceId} not found.`);
            continue; // 跳过该连线
          }
          if (!targetNodeExists) {
            console.error(`Target node with id ${targetId} not found.`);
            continue; // 跳过该连线
          }
          lines.push({
            from: lineList[b].source,
            to: lineList[b].target,
            text: lineList[b].relate,
            lineWidth: 1,
            lineShape: 1,
          })
        }
      }
      this.demoData = {
        "rootId": "4733",
        "nodes": nodes,
        "lines": lines
      }
    },


    resetGraph(){
      this.$refs.graphRef.setOptions(this.graphOptions, () => {
        this.showGraph();
      });
    }
  },
  mounted() {
    this.resetGraph();
  },
  created() {

  }
}
</script>
<style scoped>

.c-my-panel{
  width: 400px;
  position: absolute;
  left: 10px;
  top: 10px;
  border-radius: 10px;
  z-index: 800;
  background-color: #efefef;
  border: #eeeeee solid 1px;
  padding: 10px;
  .c-option-name{
    color: #666666;
    font-size: 14px;
    line-height: 40px;
    padding-left:10px;
    padding-right:10px;
  }
  .c-my-options {
    text-align: center;
    .c-my-option-item {
      text-align: left;
      color: #1da9f5;
      cursor: pointer;
      border-radius: 5px;
      padding-left: 10px;
      margin-top: 5px;
      line-height: 25px;
      &:hover{
        background-color: rgba(29, 169, 245, 0.2);
      }
    }
  }
}
</style>
