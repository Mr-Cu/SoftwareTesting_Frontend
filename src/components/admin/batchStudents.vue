<template>
  <el-card >
    <div class="biaoti">批量导入学生列表：</div>
  <el-form ref="form" :model="form" >
    <el-form-item label="文件" required>
      <el-upload
        class="upload-demo"
        :on-preview="handlePreview"
        :on-remove="handleRemove"
        action=""
        :file-list="fileList"
        :http-request="UploadAndAdd"
        :before-upload="BeforeUpload"
        drag
        multiple
      >
        <i class="el-icon-upload"></i>
        <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
        <div class="el-upload__tip" slot="tip">支持的文件格式有：xls,xlsx,学工号信息请以字符串形式存储</div>
      </el-upload>
    </el-form-item>
  </el-form>
  </el-card >
</template>

<style scoped>
.biaoti{
  font-size: 25px;
  margin-bottom: 100px;
  margin-top: 120px;
  margin-left: 70px;
}
.abc{
  position: absolute;
  left: 50%;
  top: 30%;
  transform: translate(-50%,-50%);
}
.el-card {
  padding: 1%;
  width: 50%;
  margin-left: 20%;

  /* position: absolute;
   left: 50%;
   transform: translateX(-50%); */
  background-color: rgba(255, 255, 255, 0.562);
  border-radius: 20px;
  box-shadow: 10px 10px 20px #a0a0a0;
  border-radius: 20px;
}
</style>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      newFile: new FormData(), //   1. 定义一个newFile变量（FormData 对象）
      path: ''
    }
  },
  methods: {
    handleRemove (file, fileList) {
      console.log(file, fileList)
    },
    handlePreview (file) {
      console.log(file)
    },
    BeforeUpload (file) {
      if (file) {
        this.newFile.append('file', file) //  2. 上传之前，拿到file对象，并将它添加到刚刚定义的FormData对象中。
        console.log(this.newFile.get('file'))
      } else {
        return false
      }
    },
    async UploadAndAdd () {
      const newData = this.newFile //  3. 拿到刚刚的数据，并将其传给后台
      await axios({
        url: 'http://114.55.35.220:8081/api/uploadFileUser',
        method: 'post',
        data: newData,
        headers: {
          'Content-Type': 'multipart/form-data'
        }
      })
        .then((res) => {
          this.$message.success('上传成功')
          this.path = res.data.path
          // console.log('res:', res)
        })
        .catch((err) => {
          this.$message.error('上传失败')
          console.log(err)
        })

      const url = '/post/students?filePath=' + this.path
      await axios.post(url)
        .then(
          (res) => {
            this.$message.success('学生添加成功')
            console.log(res)
          }
        )
        .catch(
          (err) => {
            this.$message.error('学生添加失败')
            console.log(err)
          }
        )
    },
    clear () {
      this.$refs.form.resetFields()
    }
  }
}
</script>
