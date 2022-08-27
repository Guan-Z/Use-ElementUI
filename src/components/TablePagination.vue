<template>
  <div class="component_box">
    <p class="title">{{tablePaginationTitle}}</p>
    <el-table
      :data="list"
      tooltip-effect="light"
      height="300"
    >
      <el-table-column prop="name" label="姓名" align="center" width="100">
      </el-table-column>
      <el-table-column prop="gender" label="性别" align="center" width="100">
      </el-table-column>
      <el-table-column prop="age" label="年龄" align="center" width="100">
      </el-table-column>
      <el-table-column prop="jobType" label="岗位" align="center" width="100">
      </el-table-column>
    </el-table>
    <div class="block">
      <!-- <span class="demonstration">完整功能</span> -->
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :pager-count="5"
        :page-sizes="[5, 10, 15, 20]"
        :page-size="5"
        layout="total, sizes, prev, pager, next, jumper"
        :total="dataList.length">
      </el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TablePagination',
  props: {
    tablePaginationTitle: String
  },
  data() {
    return {
      dataList: [
        {name: '枫叶1',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶2',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶3',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶4',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶5',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶6',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶7',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶8',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶9',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶10',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶11',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶12',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶13',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶14',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶15',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶16',gender: '男',jobType: '前端',age: 19},
        {name: '枫叶17',gender: '男',jobType: '前端',age: 19}
      ],
      list: [],
      pageNum: 1,
      pageSize: 5,
      currentPage:1
    }
  },
  methods: {
    // 真是的项目应该是前端给 pageNum 和 pageSize 作为参数给后端，
    // 即 当前页 和 当前每页多少条数据 ；具体就是更新参数然后调用getList方法
    // 分页是需要后端配合的，这样才是避免了防止一次请求过多

    // 下面只是前端效果
    handleSizeChange(val) {
      this.pageSize = val;
      console.log(`每页 ${val} 条`);
      this.list = this.dataList.slice((this.pageNum-1)*this.pageSize,(this.pageNum-1)*this.pageSize+this.pageSize);
      console.log(this.list)
      console.log((this.pageNum-1)*5)
    },
    handleCurrentChange(val) {
      this.pageNum = val;
      this.currentPage = val
      console.log(`当前页: ${val}`);
      this.list = this.dataList.slice((this.pageNum-1)*this.pageSize,(this.pageNum-1)*this.pageSize+this.pageSize);
      console.log(this.list)
      console.log((this.pageNum-1)*5)
    }
  },
  // 生命周期钩子函数不是写在methods里的
  mounted() {
    this.list = this.dataList.slice(0,this.pageSize);
  }
}
</script>

<style scoped>
.title{
  color: #777777;
}
</style>
