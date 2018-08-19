<template>
  <div class="EleTree">
    <!--<el-input-->
    <!--placeholder="输入关键字进行过滤"-->
    <!--v-model="filterText">-->
    <!--</el-input>-->

    搜索：<input type="text" placeholder="输入关键字进行过滤" v-model="filterText">

    <div class="box">
      <el-tree
        class="filter-tree"
        :data="data2"
        :props="defaultProps"
        default-expand-all
        :filter-node-method="filterNode"
        ref="tree2">
      </el-tree>
    </div>
  </div>
</template>

<script>
  export default {
    name: "EleTree",
    watch: {
      filterText(val) {
        this.$refs.tree2.filter(val);
      }
    },

    methods: {
      filterNode(value, data) {
        if (!value) return true;
        return data.label.indexOf(value) !== -1;
      }
    },

    data() {
      return {
        filterText: '',
        data2: [{
          id: 1,
          label: 'sunway 1',
          children: [{
            id: 4,
            label: 'sunway 1-1',
            children: [{
              id: 9,
              label: 'sunway 1-1-1'
            }, {
              id: 10,
              label: 'sunway 1-1-2'
            }]
          }]
        }, {
          id: 2,
          label: 'sunway 2',
          children: [{
            id: 5,
            label: 'sunway 2-1'
          }, {
            id: 6,
            label: 'sunway 2-2'
          }]
        }, {
          id: 3,
          label: 'sunway 3',
          children: [{
            id: 7,
            label: 'sunway 3-1'
          }, {
            id: 8,
            label: 'sunway 3-2'
          }]
        }],
        defaultProps: {
          children: 'children',
          label: 'label'
        }
      };
    }
  }
</script>

<style>
  .box {
    margin: 20px auto;
    width: 30%;
  }
  .el-tree-node__content {
    height: 50px;
  }
  .el-tree-node__label {
    font-size: 20px;
  }
  .el-icon-caret-right:before {
    content:'';
    background-image: url('../../static/s.png');
    background-position: center center;
    -webkit-background-size: contain;
    background-size: contain;
    width: 20px;
    height: 20px;
    display: block;
  }
</style>
