<template>
  <div>
    <button @click="generateWordFromTemplate">根据模板生成Word</button>
  </div>
</template>

<script>
import axios from 'axios';
import {getToken} from "@/utils/auth";
import {getGz} from "@/api/baogao";

export default {
  data() {
    return {
      gzList:[],
      // 动态表格数据 - 行列不定
      dynamicTableData: {
        tableTitle: "环境因素",
        headers: ["海域", "编号", "能见度", "云高", "风向","风速"],
        rows: [
          ["海域1", 1, 300, 400, 500,12],
          ["海域2", 2, 500, 200, 200,12],
          ["海域3", 3, 700, 300, 500,12],
          ["海域4", 4, 900, 500, 300,12]
          // 可以动态添加更多行
        ],

      },



      dynamicTableData1: {
        tableTitle: "载荷",
        headers: ["名称", "装备", "备注"],
        rows: [
          ["载荷1","装备1","hjdkashdjka"],
          ["载荷2","装备2","hjdkashdjka"],
          ["载荷3","装备3","hjdkashdjka"],
          // 可以动态添加更多行
        ],

      }


    };
  },
  methods: {
    getGzList(){
      var data = {}
      getGz(data).then((res)=>{
        console.log(res);
      })
    },
    async generateWordFromTemplate() {
      this.testList = [];
      this.testList.push(this.dynamicTableData);
      this.testList.push(this.dynamicTableData1);
      console.log(this.testList)
      var task = {
        "taskName":"任务1",
        "taskDesc":"任务描述一"
      }
      var data = {
        "tableData":this.testList,
        "textData":task
      }
      try {
        const response = await axios.post(
            '\n' +
            'http://localhost:10035/api/generate-word-from-template',
            data,
            {
              responseType: 'blob', // 重要：接收二进制流
              headers: {'Authorization': 'Bearer ' + getToken()},
            }
        );

        // 创建下载链接
        const url = window.URL.createObjectURL(new Blob([response.data]));
        const link = document.createElement('a');
        link.href = url;
        link.setAttribute('download', '员工绩效表_生成的.docx');
        document.body.appendChild(link);
        link.click();

        // 清理
        document.body.removeChild(link);
        window.URL.revokeObjectURL(url);
      } catch (error) {
        console.error('生成Word失败:', error);
        alert('生成Word文档失败，请检查控制台日志');
      }
    }
  }
};
</script>