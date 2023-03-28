<template>
  <div>
    <el-input v-model="searchText" placeholder="项目名" class="search-input"></el-input>
    <el-button type="primary" class="add-btn">搜索</el-button>
    <el-table :data="projects" class="project-table" @row-click="handleRowClick">
      <el-table-column prop="name" label="名称"></el-table-column>
      <el-table-column prop="time" label="时间"></el-table-column>
      <el-table-column prop="similarMethods" label="相似方法数"></el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="viewDetails(scope.$index)">查看详情</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchText: '',
      projects: [
        { name: 'codeDemo', time: '2023-02-12', similarMethods: 2 },
        { name: 'ssm', time: '2023-02-12', similarMethods: 8 },
        { name: 'codeTest', time: '2023-02-13', similarMethods: 4 },
      ],
    }
  },
  methods: {
    handleRowClick(row) {
      // 跳转到项目详情页
      this.$router.push('/codeSimDetect/projects/1')
    },
    viewDetails(index) {
      // 根据索引跳转到相应的项目详情页
      this.$router.push(`/codeSimDetect/projects/${index + 1}`)
    },
  },
}
</script>

<style scoped>
.search-input {
  width: 200px;
  margin-right: 10px;
}
.add-btn {
  margin-right: 10px;
}
.project-table {
  margin-top: 20px;
}
</style>
