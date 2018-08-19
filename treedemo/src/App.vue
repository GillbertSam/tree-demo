<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
     <h2>Sunway Tree-Demo</h2>
     <!--搜索：<input type="text" placeholder="请输入搜索类目" v-model="val" @keyup.enter="search()">-->
     <!--<button @click="search()" >search</button>-->
     <!--<p>{{msg}}</p>-->
    <!--<tree-demo @judge="showBox($event)" :datas="lists"></tree-demo>-->




    <ele-tree></ele-tree>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld'
import TreeDemo from "./components/TreeDemo";
import EleTree from "./components/EleTree";
/*
let lists = [
  {
    item: "a",
    children: [{ name: "a1" }, { name: "a2" }, { name: "a3" }],
    show: false
  },
  {
    item: "b",
    children: [{ name: "d1" }, { name: "e2" }, { name: "a3" }],
    show: false
  },
  {
    item: "c",
    children: [{ name: "b1" }, { name: "c2" }, { name: "a3" }],
    show: false
  },
  {
    item: "d",
    children: [{ name: "c1" }, { name: "b2" }, { name: "a3" }],
    show: false
  },
  {
    item: "e",
    children: [{ name: "a1" }, { name: "d2" }, { name: "a3" }],
    show: false
  }
];
*/
export default {
  name: "App",
  components: {
    TreeDemo,EleTree
  },
  data() {
    return {
      selectValue: "",
      val: "",
      lists: [],
      msg:
        "a3为公共选项卡，搜索a1,b1--c2,d2排列组合选项只会展示一栏,输入a-e分类名，展示对应选项卡内容"
    };
  },
  mounted() {
    // this.lists = lists;
  },
  methods: {
    search: function() {
      // console.log(this.val); //val 搜索值
      if (!this.val && this.val == this.selectValue) {
        return;
      }
      this.selectValue = this.val;
      this.judgeMethod();
    },
    showBox: function(index) {
      this.lists[index].show = !this.lists[index].show;
    },
    judgeMethod: function() {
      //查询匹配数据
      let tempArr = [];
      for (let k = 0; k < this.lists.length; k++) {
        console.log(this.lists[k]);
        if (this.lists[k].item.indexOf(this.val) != -1) {
          tempArr.push(k);
        }
        if (
          this.lists[k].children &&
          typeof this.lists[k].children == "object"
        ) {
          for (let j in this.lists[k].children) {
            if (this.lists[k].children[j].name.indexOf(this.val) != -1) {
              //name匹配
              if (tempArr.indexOf(k) == -1) {
                tempArr.push(k);
              }
            }
          }
        }
      }
      this.lists.forEach((v, i) => {
        v.show = false;
      });
      if (!tempArr.length) {
        alert("暂无此选项");
      } else {
        for (let i = 0; i < tempArr.length; i++) {
          this.lists[tempArr[i]].show = true;
        }
      }
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  user-select: none;
}
input {
  margin: 20px 0;
}
</style>
