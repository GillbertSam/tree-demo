<template>
 <div id="tree-demo">
     <!-- <ul v-if="lists.length > 0">
         <li v-for="(list,index) in lists" :key="index">
             <p>{{list.item}}</p>
             <span>{{list.lists}}</span>
             <TreeDemo v-if="list.children && list.children.length > 0">
                 <li v-for="(list,index) in list.children" :key="index">
                     <p>{{list.item}}</p>
                 </li>
             </TreeDemo>
             <p v-else></p>
         </li>
     </ul> -->

     <ul>
         <li v-for="(list,index) in datas" :key="index">
             <h5 @click="showBox(index)" class="title">{{list.item}}</h5>
             <div class="box" :class="{show:list.show}">
                 <p v-for="(item,index) in list.children" :key="index">
                     {{item.name}}
                 </p>
             </div>
         </li>
     </ul>
 </div>
</template>

<script type="text/ecmascript-6">
export default {
  name: "TreeDemo",
  props: ["select", "datas"],
  data() {
    return {
      //   lists: [
      //     { item: "a", children: [{ name: "1" }, { name: "2" }, { name: "3" }] ,show:false },
      //     { item: "b", children: [{ name: "1" }, { name: "2" }, { name: "3" }] ,show:false },
      //     { item: "c", children: [{ name: "1" }, { name: "2" }, { name: "3" }] ,show:false },
      //     { item: "d", children: [{ name: "1" }, { name: "2" }, { name: "3" }] ,show:false},
      //     { item: "e", children: [{ name: "1" }, { name: "2" }, { name: "3" }] ,show:false}
      //   ]
    };
  },
  components: {},
  methods: {
    showBox(index){
        this.$emit('judge',index)
    },
  },
  mounted() {}
};
</script>

<style scoped>
#tree-demo {
  width: 15%;
  border: 1px solid #ccc;
  /* margin-left: 5px; */
  margin: 20px auto;
}
#tree-demo ul {
  list-style-type: none;
}
#tree-demo ul li {
  border: 1px dashed #2dd;
}
.title {
  font-size: 24px;
}
.box {
  height: 0;
  overflow: hidden;
  transition: all 0.5s ease;
  -webkit-transition: all 0.5s ease;
}
.box.show {
  height: 60px;
}
.box p {
  border: 1px dotted #e8e8e8;
}
</style>
