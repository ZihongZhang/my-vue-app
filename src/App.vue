<template>
  <el-form ref="formRef " label-position="top" :model="form" :rules="rules" label-width="100px">
    <el-row :gutter="20">
      <el-col :span="8">
        <el-form-item label="品名规格（中文）" prop="specificationZh">
          <el-input v-model="form.specificationZh"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item label="品名规格（英文）" prop="specificationEn">
          <el-input v-model="form.specificationEn"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item label="实物图片">
          <el-upload
            class="upload-demo"
            action=""
            :auto-upload="false"
            list-type="picture-card"
            :on-preview="handlePictureCardPreview"
            :on-remove="handleRemove"
            :before-upload="beforeUpload"
            :limit="1"
            :on-exceed="handleExceed"
            :file-list="fileList">
            <i class="el-icon-plus"></i>
          </el-upload>
        </el-form-item>
      </el-col>
    </el-row>

    <el-row :gutter="20">
      <el-col :span="8">
        <el-form-item label="厂别">
          <div>
            <el-checkbox v-model="form.icc">ICC</el-checkbox>
            <el-checkbox v-model="form.imp">IMP</el-checkbox>
            <el-checkbox v-model="form.iec">IEC</el-checkbox>
            <el-checkbox v-model="form.ith">ITH</el-checkbox>
          </div>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item label="是否董事会项目" prop="boardProject">
          <el-radio-group v-model="form.boardProject">
            <el-radio label="是">是</el-radio>
            <el-radio label="否">否</el-radio>
          </el-radio-group>
        </el-form-item>
      </el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="6">
        <el-form-item label="料号类别" prop="materialCategory">
          <el-select v-model="form.materialCategory" placeholder="请选择">
            <el-option label="选项1" value="option1"></el-option>
            <el-option label="选项2" value="option2"></el-option>
          </el-select>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="购买频率" prop="purchaseFrequency">
          <el-select v-model="form.purchaseFrequency" placeholder="请选择">
            <el-option label="选项1" value="option1"></el-option>
            <el-option label="选项2" value="option2"></el-option>
          </el-select>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="是否有类似购买记录" prop="similarPurchaseRecord">
          <el-select v-model="form.similarPurchaseRecord" placeholder="请选择">
            <el-option label="是" value="yes"></el-option>
            <el-option label="否" value="no"></el-option>
          </el-select>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="类似购买记录详细说明" prop="similarPurchaseDetails">
          <el-input v-model="form.similarPurchaseDetails" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
    </el-row>

    <el-row :gutter="20">
      <el-col :span="6">
        <el-form-item label="品牌" prop="brand">
          <el-input v-model="form.brand" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="型号" prop="model">
          <el-input v-model="form.model" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="规格尺寸" prop="specifications">
          <el-input v-model="form.specifications" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="参数" prop="parameters">
          <el-input v-model="form.parameters" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
    </el-row>

    <el-row :gutter="20">
      <el-col :span="6">
        <el-form-item label="功能" prop="functionality">
          <el-input v-model="form.functionality" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="性能" prop="performance">
          <el-input v-model="form.performance" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="是否有电机" prop="hasMotor">
          <el-select v-model="form.hasMotor" placeholder="请选择">
            <el-option label="是" value="yes"></el-option>
            <el-option label="否" value="no"></el-option>
          </el-select>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="能效等级" prop="energyEfficiency">
          <el-select v-model="form.energyEfficiency" placeholder="请选择">
            <el-option label="A+" value="A+"></el-option>
            <el-option label="A" value="A"></el-option>
            <el-option label="B" value="B"></el-option>
          </el-select>
        </el-form-item>
      </el-col>
    </el-row>

    <el-row :gutter="20">
      <el-col :span="6">
        <el-form-item label="电机说明" prop="motorDescription">
          <el-input v-model="form.motorDescription" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="使用部门" prop="department">
          <el-select v-model="form.department" placeholder="请选择">
            <el-option label="部门1" value="dept1"></el-option>
            <el-option label="部门2" value="dept2"></el-option>
            <el-option label="部门3" value="dept3"></el-option>
          </el-select>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="其他部门" prop="otherDepartments">
          <el-input v-model="form.otherDepartments" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="6">
        <el-form-item label="附件" prop="attachment">
          <el-upload
            class="upload-demo"
            action=""
            :auto-upload="false"
            list-type="picture-card"
            :on-preview="handlePictureCardPreview"
            :on-remove="handleRemove"
            :before-upload="beforeUpload"
            :limit="1"
            :on-exceed="handleExceed"
            :file-list="fileList">
            <i class="el-icon-plus"></i>
          </el-upload>
        </el-form-item>
      </el-col>
    </el-row>

    <el-row :gutter="20">
      <el-col :span="24">
        <el-form-item label="备注" prop="remarks">
          <el-input type="textarea" v-model="form.remarks" placeholder="请输入"></el-input>
        </el-form-item>
      </el-col>
    </el-row>

    <el-row>
      <el-col :span="24">
        <el-form-item>
          <el-button type="primary" @click="submitForm">提交</el-button>
        </el-form-item>
      </el-col>
    </el-row>

    
  </el-form>
</template>

<script setup>
import { ref, reactive } from 'vue'

const formRef = ref(null)
const form = reactive({
  specificationZh: '',
  specificationEn: '',
  icc: false,
  imp: false,
  iec: false,
  ith: false,
  boardProject: '否',
  // 其他表单项
})

const rules = reactive({
  specificationZh: [
    { required: true, message: '请输入品名规格（中文）', trigger: 'blur' },
  ],
  specificationEn: [
    { required: true, message: '请输入品名规格（英文）', trigger: 'blur' },
  ],
  boardProject: [
    { required: true, message: '请选择是否为董事会项目', trigger: 'change' },
  ],
  // 其他验证规则
})

const fileList = ref([])

const submitForm = () => {
  formRef.value.validate((valid) => {
    if (valid) {
      console.log('提交成功:', form)
    } else {
      console.log('请检查输入')
    }
  })
}

const resetForm = () => {
  formRef.value.resetFields()
}

const handleRemove = (file, fileList) => {
  console.log(file, fileList)
}

const handlePictureCardPreview = (file) => {
  console.log(file)
}

const beforeUpload = (file) => {
  console.log(file)
  return false
}

const handleExceed = (files, fileList) => {
  console.log(files, fileList)
}
</script>

<style scoped>
.upload-demo {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
</style>