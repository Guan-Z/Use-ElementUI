<template>
  <div class="component_box">
    <p class="title">{{formTableTitle}}</p>
    <!-- model是表单数据对象，所以得是对象{}，不然报错；所以表单套表格：表格数组得放在表单对象中 -->
    <el-form :model="form" ref="dataList">
      <el-table
        :data="form.dataList"
        tooltip-effect="light"
      >
        <el-table-column prop="name" label="姓名" align="center" width="100">
        </el-table-column>
        <el-table-column prop="gender" label="性别" align="center" width="100">
          <template slot-scope="scope">
            <span class="gender_m" v-show="scope.row.gender === 0">男</span>
            <span class="gender_w" v-show="scope.row.gender === 1">女</span>
          </template>
        </el-table-column>
        <el-table-column prop="department" label="部门" align="center" width="100">
          <template slot-scope="scope">
            <div v-for="item in departmentArray" :key="item.dictValue">
              <p v-show="scope.row.department === item.dictValue">
                {{ item.dictLabel }}
              </p>
            </div>
          </template>
        </el-table-column>
        <el-table-column label="岗位" align="center" width="230">
          <template slot-scope="scope">
            <el-form-item
              :rules="[
                {
                  required: true,
                  message: '请选择岗位',
                  trigger: 'bar'
                }
              ]"
            >
              <el-select
                v-model="scope.row.jobType"
                clearable
                placeholder="请选择岗位"
              >
                <el-option
                  v-for="item in jobTypeArray"
                  :key="item.dictValue"
                  :label="item.dictLabel"
                  :value="item.dictValue"
                >
                </el-option>
              </el-select>
            </el-form-item>
          </template>
        </el-table-column>
      </el-table>
    </el-form>
    <!-- <div>
      <el-button size="mini" type="primary" @click="confirm" >确 定</el-button>
      <el-button size="mini" @click="cancel">取 消</el-button>
    </div> -->
  </div>
</template>

<script>
export default {
  name: 'FormTable',
  props: {
    formTableTitle: String
  },
  data() {
    return {
      form: {
        dataList: [
          {name: '枫叶',gender: 0,jobType: '1',department: '1'},
          {name: '白鸢',gender: 1,jobType: '2',department: '0'},
          {name: '蓝风',gender: 1,department: '2'},
        ],
      },
      jobTypeArray: [
        {dictLabel: '前端',dictValue: '1'},
        {dictLabel: '后端',dictValue: '2'},
        {dictLabel: '大数据',dictValue: '3'},
      ],
      departmentArray: [
        {dictLabel: '未知',dictValue: '0'},
        {dictLabel: '部门1',dictValue: '1'},
        {dictLabel: '部门2',dictValue: '2'},
        {dictLabel: '部门3',dictValue: '3'}
      ]
    }
  },
  methods: {
    // confirm(){
    // },
    // cancel(){
    // }
  }
}
</script>

<style scoped>
.title{
  color: #777777;
}
.gender_m{
  color: #409EFF;
}
.gender_w{
  color: #FA5151;
}
</style>
