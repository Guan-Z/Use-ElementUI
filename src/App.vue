<template>
<div class="page">
  <el-row>
    <el-col :span="24"><h2 class="title zebra_shadowText">Element-UI&nbsp;表格篇</h2></el-col>
  </el-row>
  <el-row :gutter="20">
    <el-col :span="8">
      <div class="com_box">
        <FormTable formTableTitle="表单嵌套表格"/>
      </div>
    </el-col>
    <el-col :span="8">
      <div class="com_box">
        <TablePagination tablePaginationTitle="表格配合分页"/>
      </div>
    </el-col>
    <el-col :span="8">
      <div class="com_box">
        <DeleteTableRow deleteTableRowTitle="单行、多行删除；反选和取消勾选"/>
      </div>
    </el-col>
  </el-row>
  <el-row>
    <el-col :span="24"><h2 class="title zebra_shadowText">Element-UI&nbsp;表单篇</h2></el-col>
  </el-row>
  <!-- <el-row>
    <el-col :span="24"><div class="">以上三种效果结合使用的场景如下</div></el-col>
  </el-row>
  <el-row>
    <el-col :span="24"><div class="grid-content bg-purple-dark"></div></el-col>
  </el-row> -->
</div>
</template>

<script>
import FormTable from './components/FormTable.vue';
import TablePagination from './components/TablePagination.vue';
import DeleteTableRow from './components/DeleteTableRow.vue';

export default {
  name: 'App',
  components: {
    FormTable,
    TablePagination,
    DeleteTableRow
  }
}
</script>

<style>
.page{
  min-height: 100vh;
  padding: 20px;
  background: linear-gradient(-45deg, #ee7752, #8eb3eb, #23a6d5, #b8f7c1, #b166ee);
  background-size: 800% 200%;
  animation: gradientBG 17s ease infinite;
}
@keyframes gradientBG {
  0% {
      background-position: 0% 50%;
  }
  50% {
      background-position: 100% 50%;
  }
  100% {
      background-position: 0% 50%;
  }
}
.com_box{
  padding: 20px;
  height: 400px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
  background-color: #fff;
}
.zebra_shadowText {
  font-size: 30px;
  font-weight: bold;
  /* 本身透明 */
  color: transparent;
  -webkit-text-fill-color: transparent;
  /* 阴影向上 */
  text-shadow: 6px -6px #000, 4px -4px #fff;
  /* 背景图片使用黑白渐变 */
  background-image: linear-gradient(135deg, #fff 0%, #fff 25%, #000 25%, #000 50%, #fff 50%, #fff 75%, #000 75%, #000 100%);
  background-size: 6px 6px;
  background-repeat: repeat;
  /* 背景裁剪为text裁剪 */
  background-clip: text;
}
</style>
