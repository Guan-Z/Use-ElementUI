<template>
  <div class="component_box">
    <p class="title">{{deleteTableRowTitle}}</p>
    <el-table
      ref="multipleTable"
      :data="dataList"
      tooltip-effect="dark"
      @selection-change="handleSelectionChange">
      <!-- 勾选列 -->
      <el-table-column
        fixed="left"
        type="selection"
        width="50">
      </el-table-column>
      <el-table-column
        prop="id"
        label="id"
        width="50">
      </el-table-column>
      <el-table-column
        prop="name"
        label="姓名">
      </el-table-column>
      <el-table-column
        prop="gender"
        label="性别">
      </el-table-column>
      <el-table-column
        prop="jobType"
        label="岗位">
      </el-table-column>
      <el-table-column
        prop="age"
        label="年龄">
      </el-table-column>
      <el-table-column
        prop="text"
        width="300"
        label="xxx">
      </el-table-column>
      <el-table-column
        fixed="right"
        label="操作"
        width="120">
        <template slot-scope="scope">
          <!-- @click.native.prevent -->
          <!-- 1.给vue组件绑定事件时候，组件加上.native才能监听原生事件，否则会认为监听的是来自Item组件自定义的事件，
          在封装好的组件上使用，所以要加上.native才能click
          2.prevent 是用来阻止默认的 ，相当于原生的event.preventDefault()

          根据Vue2.0官方文档关于父子组件通讯的原则，父组件通过prop传递数据给子组件，子组件触发事件给父组件。
          但父组件想在子组件上监听自己的click的话，需要加上native修饰符-->
          <el-button
            @click.native.prevent="deleteRow(scope.row.id)"
            type="text"
            size="small">
            删除
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    <div style="margin-top: 20px">
      <el-button @click="toggleSelection">反选</el-button>
      <!-- 未勾选时禁用 -->
      <!-- 绑定值的时候v-bing，所以:disabled=，不是disabled= ；其他的都是这样-->
      <el-tooltip :disabled="!disableBtn" content="勾选后才可点击" placement="bottom" effect="light">
        <span class="btn">
          <el-button @click="cancelSelection" :disabled="disableBtn">取消勾选</el-button>
        </span>
      </el-tooltip>
      <!-- 
        如何给禁用的el-button添加tooltip提示：
        el-button禁用后是不会有任何效果的，设置的tip即使没有:disabled也不展示
        所以el-button套个span(因为div会换行)，我不给el-button加tip，而是加在span上
        最后再tooltip的:disabled="!disableBtn" 和 el-button的取 “非” 就可以了
      -->
      <el-tooltip :disabled="!disableBtn" content="勾选后才可点击" placement="bottom" effect="light">
        <span class="btn">
          <el-button @click="multiSelectDelete" :disabled="disableBtn">删除</el-button>
        </span>
      </el-tooltip>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DeleteTableRow',
  props: {
    deleteTableRowTitle: String
  },
  data() {
    return {
      dataList: [
        {id: 1,name: '枫叶1',gender: '男',jobType: '前端',age: 19,text: '增加长度'},
        {id: 2,name: '枫叶2',gender: '男',jobType: '前端',age: 19,text: '增加长度'},
        {id: 3,name: '枫叶3',gender: '男',jobType: '前端',age: 19,text: '增加长度'}
      ],
      multipleSelection: [],
      disableBtn: false
    }
  },
  methods: {
    // 单个删除
    deleteRow(id) {
      alert('删除ids字段:'+id);
    },
    // 反选
    toggleSelection() {
      // 不是用选中的来做反选；反选本来就是需要遍历所有行来反选的，
      // 所以this.dataList，不是this.multipleSelection
      this.dataList.forEach(row => {
        this.$refs.multipleTable.toggleRowSelection(row);
      })
    },
    // 取消
    cancelSelection() {
      this.$refs.multipleTable.clearSelection();
    },
    // 多个删除
    multiSelectDelete() {
      let ids = '';
      for(const i of this.multipleSelection){
        ids = ids + i.id + '、';
      }
      ids = ids.slice(0,ids.length-1);
      alert('删除ids字段:'+ids);
    },
    handleSelectionChange(val) {
      this.multipleSelection = val;
      if(this.multipleSelection.length === 0){
        this.disableBtn = true;
      }else{
        this.disableBtn = false;
      }
    }
  },
  mounted() {
    if(this.multipleSelection.length === 0){
      this.disableBtn = true
    }
  }
}
</script>

<style scoped>
.title{
  color: #777777;
}
.btn{
  margin-left: 10px;
}
</style>
