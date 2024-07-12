<template>
    <h4>
      选择类目发品
    </h4>
    <el-form ref="ruleFormRef" style="max-width: 600px" :model="ruleForm" :rules="rules" label-width="auto"
      class="demo-ruleForm" :size="formSize" status-icon>
      <el-form-item label="1. 选择商品类型" prop="resource">
        <el-radio-group v-model="ruleForm.resource">
          <el-radio value="Sponsorship">现货</el-radio>
          <el-radio value="Venue">加工定制</el-radio>
        </el-radio-group>
      </el-form-item>
    </el-form>
    <el-form ref="ruleFormRef" style="max-width: 600px" :model="ruleForm" :rules="rules" label-width="auto"
      class="demo-ruleForm" :size="formSize" status-icon>
      <el-form-item label="2. 选择商品类目" prop="resource">
        <el-tree-select v-model="value" :data="data" :render-after-expand="false" style="width: 240px" />
      </el-form-item>
    </el-form>
  </template>
  
  <style>
  h4 {
    text-align: center;
  }
  </style>
  
  <script lang="ts" setup>
  import { reactive, ref } from 'vue'
  import type { ComponentSize, FormInstance, FormRules } from 'element-plus'
  
  interface RuleForm {
    resource: string
  }
  
  const formSize = ref<ComponentSize>('default')
  const ruleFormRef = ref<FormInstance>()
  const ruleForm = reactive<RuleForm>({
    resource: '',
  })
  const rules = reactive<FormRules<RuleForm>>({
    resource: [
      {
        required: true,
        message: 'Please select activity resource',
        trigger: 'change',
      },
    ],
  })
  
  const submitForm = async (formEl: FormInstance | undefined) => {
    if (!formEl) return
    await formEl.validate((valid, fields) => {
      if (valid) {
        console.log('submit!')
      } else {
        console.log('error submit!', fields)
      }
    })
  }
  
  const resetForm = (formEl: FormInstance | undefined) => {
    if (!formEl) return
    formEl.resetFields()
  }
  
  const options = Array.from({ length: 10000 }).map((_, idx) => ({
    value: `${idx + 1}`,
    label: `${idx + 1}`,
  }))
  const value = ref()
  const data = [
    {
      value: '1',
      label: 'Level one 1',
      children: [
        {
          value: '1-1',
          label: 'Level two 1-1',
          children: [
            {
              value: '1-1-1',
              label: 'Level three 1-1-1',
            },
          ],
        },
      ],
    },
    {
      value: '2',
      label: 'Level one 2',
      children: [
        {
          value: '2-1',
          label: 'Level two 2-1',
          children: [
            {
              value: '2-1-1',
              label: 'Level three 2-1-1',
            },
          ],
        },
        {
          value: '2-2',
          label: 'Level two 2-2',
          children: [
            {
              value: '2-2-1',
              label: 'Level three 2-2-1',
            },
          ],
        },
      ],
    },
    {
      value: '3',
      label: 'Level one 3',
      children: [
        {
          value: '3-1',
          label: 'Level two 3-1',
          children: [
            {
              value: '3-1-1',
              label: 'Level three 3-1-1',
            },
          ],
        },
        {
          value: '3-2',
          label: 'Level two 3-2',
          children: [
            {
              value: '3-2-1',
              label: 'Level three 3-2-1',
            },
          ],
        },
      ],
    },
  ]
  </script>