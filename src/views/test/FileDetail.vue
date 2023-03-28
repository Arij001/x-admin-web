<template>
  <div class="container">
    <h1 class="analysis-title">相似性分析</h1>
    <el-table :data="analysisData" class="analysis-table" highlight-current-row>
      <el-table-column prop="methodName" label="方法名"></el-table-column>
<!--      <el-table-column prop="similarity" label="相似度"></el-table-column>-->
      <el-table-column prop="similarity" label="相似度">
        <template v-slot="{ row }">
          <el-progress :percentage="row.similarity * 100" :status="row.similarity > 0.7 ? 'exception' : 'success'"></el-progress>
        </template>
      </el-table-column>
      <el-table-column label="源代码">
        <template v-slot="{ row }">
          <el-button type="text" size="small" @click="handleShowSourceCode(row, 'sourceCode')">查看源代码</el-button>
        </template>
      </el-table-column>
      <el-table-column label="相似方法源代码">
        <template v-slot="{ row }">
          <el-button type="text" size="small" @click="handleShowSourceCode(row, 'similarMethod')">查看相似方法源代码</el-button>
        </template>
      </el-table-column>
      <el-table-column prop="similarFile" label="相似方法所属文件"></el-table-column>
      <el-table-column prop="similarMethodName" label="相似方法名"></el-table-column>
    </el-table>
    <el-dialog title="源代码" :visible.sync="showSourceCodeDialog" width="80%">
      <pre class="source-code">{{ displayedSourceCode }}</pre>
      <div class="close-btn">
        <el-button type="primary" @click="showSourceCodeDialog = false">关闭</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
export default {
  data() {
    return {
      showSourceCodeDialog: false,
      displayedSourceCode: '',
      analysisData: [
        {
          id: 1,
          methodName: 'calculateTotalPrice',
          similarity: 0.85,
          sourceCode: `public double calculateTotalPrice(List<Product> products) {
  double totalPrice = 0;
  for (Product product : products) {
    totalPrice += product.getPrice() * product.getQuantity();
  }
  return totalPrice;
}`,
          similarMethod: `public double computeTotalPrice(List<Item> items) {
  double total = 0;
  for (Item item : items) {
    total += item.getPrice() * item.getQuantity();
  }
  return total;
}`,
          similarFile: 'Order.java',
          similarMethodName: 'computeTotalPrice',
        },
        {
          id: 2,
          methodName: 'getFullName',
          similarity: 0.80,
          sourceCode: `public String getFullName() {
  return firstName + " " + lastName;
}`,
          similarMethod: `public String generateFullName() {
  return this.firstName + " " + this.lastName;
}`,
          similarFile: 'Person.java',
          similarMethodName: 'generateFullName',
        },
      ],
    }
  },
  methods: {
    handleShowSourceCode(row, codeType) {
      this.displayedSourceCode = row[codeType]
      this.showSourceCodeDialog = true
    },
  },
}
</script>
<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
}

.analysis-title {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 20px;
}

.analysis-table {
  width: 100%;
  margin-bottom: 20px;
}

.source-code {
  font-family: 'Courier New', Courier, monospace;
  white-space: pre-wrap;
}

.close-btn {
  text-align: right;
}
</style>
