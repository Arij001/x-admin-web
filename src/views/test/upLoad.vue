<template>
  <div>
    <el-row>
      <el-col :span="24" style="text-align: center;">
        <h2>上传项目</h2>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24" style="text-align: center;">
        <el-upload
          class="upload-demo"
          drag
          action="/api/upload"
          :auto-upload="false"
          :before-upload="beforeUpload"
          :on-success="onSuccess"
        >
          <i class="el-icon-upload"></i>
          <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
        </el-upload>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24" style="text-align: center; margin-top: 20px;">
        <el-button type="primary" @click="submitProject">提交</el-button>
        <el-button type="success" @click="detect" style="margin-left: 10px;">检测</el-button>
        <el-button type="danger" @click="reset" style="margin-left: 10px;">重置</el-button>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  methods: {
    detect() {
      // 添加检测功能的实现
    },
    reset() {
      // 添加重置功能的实现
    },
  },
};
</script>

<style>
.upload-demo {
  padding: 20px;
  border: 1px dashed #20a0ff;
  background-color: #fff;
  color: #20a0ff;
  text-align: center;
  cursor: pointer;
  border-radius: 4px;
}
</style>
