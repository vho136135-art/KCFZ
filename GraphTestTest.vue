<template>
  <div class="relation-graph-demo">
    <div class="toolbar">
      <button @click="applyForceLayout">力导向布局</button>
      <button @click="applyCircleLayout">圆形布局</button>
      <button @click="applyTreeLayout">树状布局</button>
      <button @click="applyMixedLayout">混合布局</button>
    </div>

    <RelationGraph
        ref="graphRef"
        :options="graphOptions"
        @on-node-click="onNodeClick"
        @on-line-click="onLineClick"
        style="width: 80vw;height: 40vw;"
    />
  </div>
</template>

<script>
import {getgraphInfo} from "@/api/login";

export default {
  name: 'RelationGraphDemo',
  data() {
    return {
      demoData: {},
      types:[],
      graphOptions1: {
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
        lineWidth: 1,
        defaultLineWidth: 2,
        defaultLineShape: 1,
        defaultNodeShape: 0,
        defaultNodeBorderWidth: 0,
        defaultLineColor: 'rgb(255,255,255)',
        defaultNodeColor: 'rgba(0, 206, 209, 1)',
        lineLengths: 100,
        defaultNodeFontSize: '16px', // 全局默认字体大小

      },
      graphOptions: {
        defaultNodeShape: 0,
        defaultNodeWidth: 60,
        defaultNodeHeight: 60,
        defaultLineWidth: 2,
        defaultLineColor: 'rgba(100, 100, 100, 0.5)',
        allowSwitchLineShape: true,
        allowSwitchJunctionPoint: true,

        defaultLayout: {
          type: 'center',

        },
        allowNodeAutoLayout: true,
        allowCustomLayout: true
      },
      graphData: {
        nodes: [
          { id: 'center', text: '中心节点', borderColor: 'gold', isCenter: true },
          { id: 'a1', text: '圆形组1', group: 'free', color: '#ff9999' },
          { id: 'a2', text: '圆形组2', group: 'free', color: '#ff9999' },
          { id: 'a3', text: '圆形组3', group: 'free', color: '#ff9999' },
          { id: 'a4', text: '圆形组4', group: 'free', color: '#ff9999' },
          { id: 'b1', text: '树状组1', group: 'tree', color: '#99ccff' },
          { id: 'b2', text: '树状组2', group: 'tree', color: '#99ccff' },
          { id: 'b3', text: '树状组3', group: 'tree', color: '#99ccff' },
          { id: 'c1', text: '自由节点1', group: 'free', color: '#99ff99' },
          { id: 'c2', text: '自由节点2', group: 'free', color: '#99ff99' }
        ],
        links: [
          { from: 'center', to: 'a1' },
          { from: 'center', to: 'a2' },
          { from: 'center', to: 'a3' },
          { from: 'center', to: 'a4' },
          { from: 'center', to: 'b1' },
          { from: 'b1', to: 'b2' },
          { from: 'b2', to: 'b3' },
          { from: 'center', to: 'c1' },
          { from: 'center', to: 'c2' },
          { from: 'c1', to: 'c2' }
        ]
      }
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.applyMixedLayout();
    });
  },
  methods: {
    applyForceLayout() {
      this.$refs.graphRef.doLayout({
        type: 'force',
        gravity: 10,
        distance: 100
      });
    },
    applyCircleLayout() {
      this.$refs.graphRef.doLayout({
        type: 'circle',
        radius: 200
      });
    },
    applyTreeLayout() {
      this.$refs.graphRef.doLayout({
        type: 'tree',
        direction: 'right',
        levelDistance: 150
      });
    },
    applyMixedLayout() {
      const graph = this.$refs.graphRef;
      let params = {};
      getgraphInfo(params).then((res) => {
        this.zhengl(res.data);
        this.$refs.graphRef.setJsonData(this.demoData, () => {

        });
        console.log("000----")
        const allNodes = this.demoData.nodes;

        // 计算画布中心点
        const centerX = 40;
        const centerY = 200;

        // 1. 对上半部分节点应用树状布局 (Y坐标小于中心点的节点)
        const topNodes = allNodes.filter(n => n.group == "tree").map(n => n.id);

        graph.doLayout({
          type: 'tree',
          nodes: topNodes,
          direction: 'down',  // 树状布局方向向下
          levelDistance: 120,
          center: { x: centerX, y: centerY / 2 },
          animation: true,

        });

        // 2. 对下半部分节点应用力导向布局 (Y坐标大于等于中心点的节点)
        const bottomNodes = allNodes.filter( n => n.group === "free").map(n => n.id);
        console.log(bottomNodes)

        // 先设置初始位置在下半部分
        bottomNodes.forEach((nodeId) => {
          const node = allNodes.find(n => n.id === nodeId);
          if (node) {
            node.x = 200;
            node.y = 6000;
          }
        });

        // 然后应用力导向布局
        graph.doLayout({
          type: 'center',
          nodes: bottomNodes,

          center: { x: 500, y: 600 }, // 中心点偏下

        });

      })



      // 3. 对树状组节点应用树状布局

    },

    zhengl(data) {
      console.log(data)
      const nodes = []
      const lines = [] // 存放节点和关系
      var nodeList = data.nodes;
      var lineList = data.links;
      console.log(nodeList)
      if (nodeList != undefined) {
        var root = nodeList.filter(node => node.name === 'task');
        this.rootId = root.id;


        var leve0Nodes = nodeList.filter(node => node.group === '0' && node.type === 0);
        // console.log(leve0Nodes);
        var startX = -(leve0Nodes.length * 150) / 2; // 居中起始位置

        leve0Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 0,
            x: startX + index * 200, // 水平等距排列
            y: 200,                 // leve0 的固定 Y 坐标
            fixed: true,            // 固定位置
            opacity: 0,
            properties: {...node},
            ...style,
            group:"tree",
          });
        });
        var leve1Nodes = nodeList.filter(node => node.group === '1' && node.type === 0);
        var startX1 = -(leve1Nodes.length * 270) / 2; // 居中起始位置
        leve1Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startX1 + index * 270, // 水平等距排列
            y: 400,                 // leve1 的固定 Y 坐标
            fixed: true,            // 固定位置

            data: {...node},
            ...style,
            group:"tree",
          });
        });
        var leve2Nodes = nodeList.filter(node => node.group === '2' && node.type === 0);
        var startX2 = -(leve2Nodes.length * 250) / 2 - 1000; // 居中起始位置
        leve2Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 2,
            x: startX2 + index * 250, // 水平等距排列
            y: 700,                 // leve2 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style,
            group:"tree",
          });
        });
        var leve3Nodes = nodeList.filter(node => node.group === '3' && node.type === 0);
        var startX3 = -(leve3Nodes.length * 250) / 2; // 居中起始位置
        leve3Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 3,
            x: startX3 + index * 250, // 水平等距排列
            y: 1000,                 // leve3 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style,
            group:"tree",
          });
        });
        var leve4Nodes = nodeList.filter(node => node.group === '4' && node.type === 0);
        var startX4 = -(leve4Nodes.length * 250) / 2; // 居中起始位置
        leve4Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 4,
            x: startX4 + index * 250, // 水平等距排列
            y: 1500,                 // leve4 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style,
            group:"tree",
          });
        });
        var leve5Nodes = nodeList.filter(node => node.group === '5' && node.type === 0);
        // console.log(leve5Nodes)

        var startX5 = -(leve5Nodes.length * 250) / 2; // 居中起始位置
        leve5Nodes.forEach((node, index) => {
          var ggg = 0;
          if(this.types.length>0){

            for(let c=0;c<this.types.length;c++){
              if(this.types[c]==node.name){
                ggg = 1;
                break;
              }
            }
          }
          if(this.types.length>0 && ggg==1){
            const group = parseInt(node.group, 10);
            const style = this.getNodeStyle(group);
            nodes.push({
              id: node.id,
              text: node.name,
              level: 5,
              x: startX5 + index * 250, // 水平等距排列
              y: 2000,                 // leve5 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: {...node},
              ...style,
              group:"tree",

            });
          }
          if(this.types.length==0){
            const group = parseInt(node.group, 10);
            const style = this.getNodeStyle(group);
            nodes.push({
              id: node.id,
              text: node.name,
              level: 5,
              x: startX5 + index * 250, // 水平等距排列
              y: 2000,                 // leve5 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: {...node},
              ...style,
              group:"tree",
            });
          }
        });
        var leve6Nodes = nodeList.filter(node => node.group === '6' && node.type === 0);
        // console.log(leve6Nodes)
        var startX6 = -(leve6Nodes.length * 300) / 2; // 居中起始位置
        leve6Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 6,
            x: startX6 + index * 300, // 水平等距排列
            y: 2500,                 // leve6 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style,
            group:"tree",

          });
        });
        var leve7Nodes = nodeList.filter(node => node.group === '7' && node.type === 0);
        // console.log(leve7Nodes)
        var startX7 = -(leve7Nodes.length * 200) / 2; // 居中起始位置
        leve7Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 7,
            x: startX7 + index * 200, // 水平等距排列
            y: 3000,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style,
            expanded: false,
            expandHolderPosition: 'bottom',
            group:"tree",
          });
        });

        console.log(nodes);
        // var NodesText1 = nodeList.filter(node => node.group === '1' && node.type === 1);
        // // console.log(NodesText1)
        // var startText1 = - (NodesText1.length * 200) / 2; // 居中起始位置
        // NodesText1.forEach((node, index) => {
        //   nodes.push({
        //     id: node.id,
        //     text: node.name,
        //     level: 1,
        //     x: startText1 + index * 200, // 水平等距排列
        //     y: 3500,                 // leve7 的固定 Y 坐标
        //     fixed: true,            // 固定位置
        //     data: { ...node },
        //     expandHolderPosition: 'bottom',
        //     width: 180,
        //     height: 180,
        //   });
        // });
        var NodesText2 = nodeList.filter(node => node.group === '2' && node.type != 0);
        // console.log(NodesText2)
        var startText2 = -(NodesText2.length * 200) / 2; // 居中起始位置
        NodesText2.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText2 + index * 400, // 水平等距排列
            y: 7000,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            width: 180,
            height: 180,
            group:"tree",
            expandHolderPosition: 'bottom',
          });
        });
        var NodesText3 = nodeList.filter(node => node.group === '3' && node.type != 0);
        // console.log(NodesText3)
        var startText3 = -(NodesText3.length * 200) / 2; // 居中起始位置
        NodesText3.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText3 + index * 400, // 水平等距排列
            y: 7500,                 // leve7 的固定 Y 坐标
            fixed: true,                  // 固定位置
            data: {...node},
            width: 180,
            height: 180,
            group:"tree",
            expandHolderPosition: 'bottom',
          });
        });
        var NodesText4 = nodeList.filter(node => node.group === '4' && node.type != 0);
        // console.log(NodesText4)
        var startText4 = -(NodesText4.length * 200) / 2; // 居中起始位置
        NodesText4.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText4 + index * 200, // 水平等距排列
            y: 4500,                 // leve7 的固定 Y 坐标
            fixed: false,                  // 固定位置
            data: {...node},
            width: 180,
            height: 180,
            group:"free",
            expandHolderPosition: 'bottom',
          });
        });
        var NodesText5 = nodeList.filter(node => node.group === '5' && node.type != 0);
        // console.log(NodesText5)
        var startText5 = -(NodesText5.length * 200) / 2; // 居中起始位置
        NodesText5.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText5 + index * 200, // 水平等距排列
            y: 5000,                 // leve7 的固定 Y 坐标
            fixed: false,                 // 固定位置
            data: {...node},
            width: 180,
            height: 180,
            group:"free",
            expandHolderPosition: 'bottom',
          });
        });

        var NodesText6 = nodeList.filter(node => node.group === '6' && node.type != 0);
        // console.log(NodesText5)
        var startText6 = -(NodesText6.length * 200) / 2; // 居中起始位置
        NodesText6.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText6 + index * 200, // 水平等距排列
            y: 5500,                 // leve7 的固定 Y 坐标
            fixed: false,                  // 固定位置
            data: {...node},
            width: 180,
            height: 180,
            group:"free",

            expandHolderPosition: 'bottom',
          });
        });


      }


      if (lineList != undefined) {
        var leve0Lines = lineList.filter(line => line.relate === '任务');
        // console.log(leve0Lines);
        leve0Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            isHide: true,
          });
        });
        var leve1Lines = lineList.filter(line => line.relate === '执行');
        // console.log(leve1Lines);
        leve1Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#90EE90',
          });
        });
        var leve2Lines = lineList.filter(line => line.relate === '约束');
        // console.log(leve2Lines);
        leve2Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#FF4500',
          });
        });
        var leve3Lines = lineList.filter(line => line.relate === '具备');
        // console.log(leve3Lines);
        leve3Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#FFA500',
          });
        });
        var leve4Lines = lineList.filter(line => line.relate === '搭载');
        // console.log(leve4Lines);
        leve4Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#00FFFF',
          });
        });
        var leve5Lines = lineList.filter(line => line.relate === '包含');
        // console.log(leve5Lines);
        leve5Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: 'white',
          });
        });
        var leve6Lines = lineList.filter(line => line.relate === '影响');
        // console.log(leve6Lines);
        leve6Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#FFFF00',
          });
        });
        var leve7Lines = lineList.filter(line => line.relate !== '任务' && line.relate !== '执行' && line.relate !== '约束' && line.relate !== '具备' && line.relate !== '搭载' && line.relate !== '包含' && line.relate !== '影响');
        console.log("属于：")
        console.log(leve7Lines)
        leve7Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#1808fa',
          });
        });
        // for (let b = 0; b < lineList.length; b++) {
        //   const sourceId = lineList[b].source;
        //   const targetId = lineList[b].target;

        //   // 检查 source 和 target 是否存在于节点的 id 中
        //   const sourceNodeExists = nodes.some(node => node.id === sourceId);
        //   const targetNodeExists = nodes.some(node => node.id === targetId);
        //   if (!sourceNodeExists) {
        //     console.error(`Source node with id ${sourceId} not found.`);
        //     continue; // 跳过该连线
        //   }
        //   if (!targetNodeExists) {
        //     console.error(`Target node with id ${targetId} not found.`);
        //     continue; // 跳过该连线
        //   }
        //   lines.push({
        //     from: lineList[b].source,
        //     to: lineList[b].target,
        //     text: lineList[b].relate,
        //     lineWidth: 1,
        //     lineShape: 1,
        //   })
        // }
      }
      this.demoData = {
        "rootId": this.rootId,
        "nodes": nodes,
        "lines": lines
      }
    },
    zhengl1(data) {
      console.log(data)
      const nodes = []
      const lines = [] // 存放节点和关系
      var nodeList = data.nodes;
      var lineList = data.links;
      console.log(nodeList)
      if (nodeList != undefined) {
        var root = nodeList.filter(node => node.name === 'task');
        this.rootId = root.id;


        var leve0Nodes = nodeList.filter(node => node.group === '0' && node.type === 0);
        // console.log(leve0Nodes);
        var startX = -(leve0Nodes.length * 150) / 2; // 居中起始位置

        leve0Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 0,
            x: startX + index * 200, // 水平等距排列
            y: 200,                 // leve0 的固定 Y 坐标
            fixed: true,            // 固定位置
            opacity: 0,

            properties: {...node},
            ...style
          });
        });
        var leve1Nodes = nodeList.filter(node => node.group === '1' && node.type === 0);
        var startX1 = -(leve1Nodes.length * 270) / 2; // 居中起始位置
        leve1Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startX1 + index * 270, // 水平等距排列
            y: 400,                 // leve1 的固定 Y 坐标
            fixed: true,            // 固定位置

            data: {...node},
            ...style
          });
        });
        var leve2Nodes = nodeList.filter(node => node.group === '2' && node.type === 0);
        var startX2 = -(leve2Nodes.length * 250) / 2 - 1000; // 居中起始位置
        leve2Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 2,
            x: startX2 + index * 250, // 水平等距排列
            y: 700,                 // leve2 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style
          });
        });
        var leve3Nodes = nodeList.filter(node => node.group === '3' && node.type === 0);
        var startX3 = -(leve3Nodes.length * 250) / 2; // 居中起始位置
        leve3Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 3,
            x: startX3 + index * 250, // 水平等距排列
            y: 1000,                 // leve3 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style
          });
        });
        var leve4Nodes = nodeList.filter(node => node.group === '4' && node.type === 0);
        var startX4 = -(leve4Nodes.length * 250) / 2; // 居中起始位置
        leve4Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 4,
            x: startX4 + index * 250, // 水平等距排列
            y: 1500,                 // leve4 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style
          });
        });
        var leve5Nodes = nodeList.filter(node => node.group === '5' && node.type === 0);
        // console.log(leve5Nodes)

        var startX5 = -(leve5Nodes.length * 250) / 2; // 居中起始位置
        leve5Nodes.forEach((node, index) => {
          var ggg = 0;
          if(this.types.length>0){

            for(let c=0;c<this.types.length;c++){
              if(this.types[c]==node.name){
                ggg = 1;
                break;
              }
            }
          }
          if(this.types.length>0 && ggg==1){
            const group = parseInt(node.group, 10);
            const style = this.getNodeStyle(group);
            nodes.push({
              id: node.id,
              text: node.name,
              level: 5,
              x: startX5 + index * 250, // 水平等距排列
              y: 2000,                 // leve5 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: {...node},
              ...style,

            });
          }
          if(this.types.length==0){
            const group = parseInt(node.group, 10);
            const style = this.getNodeStyle(group);
            nodes.push({
              id: node.id,
              text: node.name,
              level: 5,
              x: startX5 + index * 250, // 水平等距排列
              y: 2000,                 // leve5 的固定 Y 坐标
              fixed: true,            // 固定位置
              data: {...node},
              ...style,
            });
          }
        });
        var leve6Nodes = nodeList.filter(node => node.group === '6' && node.type === 0);
        // console.log(leve6Nodes)
        var startX6 = -(leve6Nodes.length * 300) / 2; // 居中起始位置
        leve6Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 6,
            x: startX6 + index * 300, // 水平等距排列
            y: 2500,                 // leve6 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style,

          });
        });
        var leve7Nodes = nodeList.filter(node => node.group === '7' && node.type === 0);
        // console.log(leve7Nodes)
        var startX7 = -(leve7Nodes.length * 200) / 2; // 居中起始位置
        leve7Nodes.forEach((node, index) => {
          const group = parseInt(node.group, 10);
          const style = this.getNodeStyle(group);
          nodes.push({
            id: node.id,
            text: node.name,
            level: 7,
            x: startX7 + index * 200, // 水平等距排列
            y: 3000,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            ...style,
            expanded: false,
            expandHolderPosition: 'bottom',
          });
        });

        console.log(nodes);
        // var NodesText1 = nodeList.filter(node => node.group === '1' && node.type === 1);
        // // console.log(NodesText1)
        // var startText1 = - (NodesText1.length * 200) / 2; // 居中起始位置
        // NodesText1.forEach((node, index) => {
        //   nodes.push({
        //     id: node.id,
        //     text: node.name,
        //     level: 1,
        //     x: startText1 + index * 200, // 水平等距排列
        //     y: 3500,                 // leve7 的固定 Y 坐标
        //     fixed: true,            // 固定位置
        //     data: { ...node },
        //     expandHolderPosition: 'bottom',
        //     width: 180,
        //     height: 180,
        //   });
        // });
        var NodesText2 = nodeList.filter(node => node.group === '2' && node.type != 0);
        // console.log(NodesText2)
        var startText2 = -(NodesText2.length * 200) / 2; // 居中起始位置
        NodesText2.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText2 + index * 400, // 水平等距排列
            y: 3500,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            width: 180,
            height: 180,
            expandHolderPosition: 'bottom',
          });
        });
        var NodesText3 = nodeList.filter(node => node.group === '3' && node.type != 0);
        // console.log(NodesText3)
        var startText3 = -(NodesText3.length * 200) / 2; // 居中起始位置
        NodesText3.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText3 + index * 400, // 水平等距排列
            y: 4000,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            width: 180,
            height: 180,

            expandHolderPosition: 'bottom',
          });
        });
        var NodesText4 = nodeList.filter(node => node.group === '4' && node.type != 0);
        // console.log(NodesText4)
        var startText4 = -(NodesText4.length * 200) / 2; // 居中起始位置
        NodesText4.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText4 + index * 200, // 水平等距排列
            y: 4500,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            width: 180,
            height: 180,

            expandHolderPosition: 'bottom',
          });
        });
        var NodesText5 = nodeList.filter(node => node.group === '5' && node.type != 0);
        // console.log(NodesText5)
        var startText5 = -(NodesText5.length * 200) / 2; // 居中起始位置
        NodesText5.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText5 + index * 200, // 水平等距排列
            y: 5000,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            width: 180,
            height: 180,

            expandHolderPosition: 'bottom',
          });
        });

        var NodesText6 = nodeList.filter(node => node.group === '6' && node.type != 0);
        // console.log(NodesText5)
        var startText6 = -(NodesText6.length * 200) / 2; // 居中起始位置
        NodesText6.forEach((node, index) => {
          nodes.push({
            id: node.id,
            text: node.name,
            level: 1,
            x: startText6 + index * 200, // 水平等距排列
            y: 5500,                 // leve7 的固定 Y 坐标
            fixed: true,            // 固定位置
            data: {...node},
            width: 180,
            height: 180,

            expandHolderPosition: 'bottom',
          });
        });


      }


      if (lineList != undefined) {
        var leve0Lines = lineList.filter(line => line.relate === '任务');
        // console.log(leve0Lines);
        leve0Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            isHide: true,
          });
        });
        var leve1Lines = lineList.filter(line => line.relate === '执行');
        // console.log(leve1Lines);
        leve1Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#90EE90',
          });
        });
        var leve2Lines = lineList.filter(line => line.relate === '约束');
        // console.log(leve2Lines);
        leve2Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#FF4500',
          });
        });
        var leve3Lines = lineList.filter(line => line.relate === '具备');
        // console.log(leve3Lines);
        leve3Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#FFA500',
          });
        });
        var leve4Lines = lineList.filter(line => line.relate === '搭载');
        // console.log(leve4Lines);
        leve4Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#00FFFF',
          });
        });
        var leve5Lines = lineList.filter(line => line.relate === '包含');
        // console.log(leve5Lines);
        leve5Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: 'white',
          });
        });
        var leve6Lines = lineList.filter(line => line.relate === '影响');
        // console.log(leve6Lines);
        leve6Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#FFFF00',
          });
        });
        var leve7Lines = lineList.filter(line => line.relate !== '任务' && line.relate !== '执行' && line.relate !== '约束' && line.relate !== '具备' && line.relate !== '搭载' && line.relate !== '包含' && line.relate !== '影响');
        console.log("属于：")
        console.log(leve7Lines)
        leve7Lines.forEach(line => {
          lines.push({
            from: line.source,
            to: line.target,
            text: line.relate,
            lineWidth: 2,
            lineShape: 1,
            color: '#1808fa',
          });
        });
        // for (let b = 0; b < lineList.length; b++) {
        //   const sourceId = lineList[b].source;
        //   const targetId = lineList[b].target;

        //   // 检查 source 和 target 是否存在于节点的 id 中
        //   const sourceNodeExists = nodes.some(node => node.id === sourceId);
        //   const targetNodeExists = nodes.some(node => node.id === targetId);
        //   if (!sourceNodeExists) {
        //     console.error(`Source node with id ${sourceId} not found.`);
        //     continue; // 跳过该连线
        //   }
        //   if (!targetNodeExists) {
        //     console.error(`Target node with id ${targetId} not found.`);
        //     continue; // 跳过该连线
        //   }
        //   lines.push({
        //     from: lineList[b].source,
        //     to: lineList[b].target,
        //     text: lineList[b].relate,
        //     lineWidth: 1,
        //     lineShape: 1,
        //   })
        // }
      }
      this.demoData = {
        "rootId": this.rootId,
        "nodes": nodes,
        "lines": lines
      }
    },
    getNodeStyle(group) {
      const styles = [
        {width: 150, height: 150, color: "#ef7a43", fontColor: '255,255,255', size: '60px'},
        {width: 250, height: 250, color: '#ffa384', font: 'normal 40px Arial', fontColor: '0,0,0'},
        {width: 230, height: 230, color: '#00f6ff', font: 'normal 50px Arial', fontColor: '0,0,0'},
        {width: 210, height: 210, color: '#00c6ff', font: 'normal 40px Arial', fontColor: '0,0,0'},
        {width: 200, height: 200, color: '#2a98ff', font: 'normal 32px Arial', fontColor: '#ffffff'},
        {width: 200, height: 200, color: '#005fb7', font: 'normal 30px Arial', fontColor: '#ffffff'},
        {width: 200, height: 200, color: '#003ea4', font: 'normal 28px Arial', fontColor: '#ffffff'},
        {width: 190, height: 190, color: '#7df887', font: 'normal 28px Arial', fontColor: '#000000'}
      ];

      return styles[group] || {};
    },
    onNodeClick(node) {
      console.log('点击节点:', node);
    },
    onLineClick(line) {
      console.log('点击连线:', line);
    }
  }
};
</script>

<style scoped>
.relation-graph-demo {
  width: 100%;
  height: 800px;
  position: relative;
}

.toolbar {
  position: absolute;
  top: 10px;
  left: 10px;
  z-index: 100;
  background: rgba(255, 255, 255, 0.8);
  padding: 10px;
  border-radius: 4px;
}

.toolbar button {
  margin: 0 5px;
  padding: 5px 10px;
  cursor: pointer;
}
</style>