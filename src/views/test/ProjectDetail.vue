<template>
  <div class="container">


    <h2 class="project-title">{{ project.name }}</h2>
    <div class="search-container">
      <el-input v-model="searchText" placeholder="文件名" class="search-input"></el-input>
      <el-button type="primary" class="search-btn">搜索</el-button>
    </div>
    <el-table :data="files" class="file-table" @row-click="handleRowClick">
      <el-table-column prop="name" label="名称"></el-table-column>
      <el-table-column prop="path" label="文件路径"></el-table-column>
      <el-table-column label="是否存在相似方法">
        <template v-slot="{ row }">
          <div class="similarity-cell">
            {{ row.similarity ? '是' : '否' }}
            <el-button v-if="row.similarity" type="text" size="small" class="detail-btn" @click="handleShowSimilar(row)">查看详情</el-button>
          </div>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog title="相似文件" :visible.sync="showSimilarDialog" width="800px">
      <el-table :data="similarFiles" class="file-table">
        <el-table-column prop="name" label="名称"></el-table-column>
        <el-table-column prop="similarity" label="相似度"></el-table-column>
      </el-table>
      <div class="close-btn">
        <el-button type="primary" @click="showSimilarDialog = false">关闭</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchText: '',
      showSimilarDialog: false,
      project: { id: '1', name: 'codeDemo', type: 'Java' },
      files: [
        { id: '1', name: 'TestA.java', path: '/src/main/java/com/demo/priceCaculate.java', similarity: 0.9 },
        { id: '2', name: 'Person.java', path: '/src/main/java/com/example/文件2.java', similarity: 0.7},
        { id: '3', name: 'Order.java', path: '/src/main/java/com/example/文件3.java', similarity: 0.7 },
        { id: '4', name: 'TestB.java', path: '/src/main/java/com/example/文件3.java', similarity: 0 },
      ],
      similarFiles: [
        { id: '4', name: '文件4.java', similarity: 0.85 },
        { id: '5', name: '文件5.java', similarity: 0.83 },
        { id: '6', name: '文件6.java', similarity: 0.82 },
      ],
    }
  },
  methods: {
    handleRowClick(row) {
      // 跳转到文件详情页
      this.$router.push('/codeSimDetect/files/1')
    },
    handleShowSimilar(row) {
      event.stopPropagation() // 阻止事件冒泡
      // 显示相似文件列表
      this.similarFiles = this.getSimilarFiles(row.id)
      this.showSimilarDialog = true
    },
    getSimilarFiles(fileId) {
      // TODO: 加载相似文件列表数据
      return [
        { id: '4', name: '文件4.java', similarity: 0.85 },
        { id: '5', name: '文件5.java', similarity: 0.83 },
        { id: '6', name: '文件6.java', similarity: 0.82 },
      ]
    },
  },
}
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
}

.main-title {
  font-size: 36px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 30px;
}

.divider {
  border: none;
  border-top: 1px solid #ccc;
  margin: 20px 0;
}

.project-title {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 10px;
}

.search-container {
  display: flex;
  align-items: center;
  /*justify-content: flex-end;*/
  margin-bottom: 20px;
}

.search-input {
  width: 300px;
  margin-right: 10px;
}

.file-table {
  width: 100%;
}

.similarity-cell {
  display: flex;
  align-items: center;
}

.detail-btn {
  margin-left: 10px;
}

.close-btn {
  text-align: right;
}
</style>

