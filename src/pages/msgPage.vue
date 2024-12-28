<template>
  <div class="msg-wrap">
    <el-button>111</el-button>
    <div
      v-for="(item, index) in list"
      :key="index"
      class="msg"
      :class="[item.onlyMsgId]"
      @mouseup="mouseupHandler($event, item)"
    >
      <span>id: {{ item.id }}</span>
      <span>type: {{ item.type }}</span>
      <img
        v-if="item.type === 'photo'"
        style="width: 800px; height: 200px"
        src="https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg"
      />
      <h4>content: {{ item.content }}</h4>
    </div>
    <el-dialog
      title="收货地址"
      :visible.sync="dialogTableVisible"
      v-if="dialogTableVisible"
      append-to-body
    >
      <el-table :data="gridData">
        <el-table-column
          property="date"
          label="日期"
          width="150"
        ></el-table-column>
        <el-table-column
          property="name"
          label="姓名"
          width="200"
        ></el-table-column>
        <el-table-column property="address" label="地址"></el-table-column>
      </el-table>
    </el-dialog>
  </div>
</template>

<script>
import genid from "genid";
import { list } from "./index.js";
import { getFirstSelection } from "first-selection";

export default {
  data() {
    return {
      list: [],
      gridData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
      ],
      dialogTableVisible: false,
    };
  },
  created() {
    this.list = list.map((item) => ({
      ...item,
      onlyMsgId: genid(),
    }));
  },
  methods: {
    clickTo() {
      this.dialogTableVisible = true;
      console.log("clickTo");
    },
    mousedownHandler(e) {
      console.log(e);
    },
    mouseupHandler(event, item) {
      // console.log(e);
      const selection = getFirstSelection(window);
      // console.log(selection);
      const { collapsed, success, firstSelectionText } = selection;
      const dom = document.getElementById("self_word-line");
      if (!collapsed && success) {
        console.log(firstSelectionText, selection.range);
        const beInsertedParent = document.getElementsByClassName(
          item.onlyMsgId
        )[0];
        beInsertedParent.appendChild(dom);
        dom.style.display = "block";
        dom.style.left = `${event.offsetX}px`;
        dom.style.top = `${event.offsetY}px`;
        dom.addEventListener("click", this.clickTo);
      } else {
        dom.style.display = "none";
      }
    },
  },
};
</script>

<style>
.msg-wrap {
  margin: 0 auto;
  padding: 24px;
  width: 1200px;
  height: 1000px;
  overflow: auto;
  border: 1px solid #ccc;
  border-radius: 16px;
}
.msg {
  border: 1px solid #ccc;
  padding: 8px;
  position: relative;
  left: 0;
}
</style>