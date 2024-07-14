<script lang="ts" setup>
import { reactive, ref, provide, } from 'vue'
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
            message: '有必选项未选择',
            trigger: 'change',
        },
    ],
})
const value = ref([])

const props = {
    expandTrigger: 'hover' as const,
}

const ttt = ref("null")
provide('ttt.value', ttt);

const handleChange = (value: any) => {
    if (ttt.value.length > 0) {
        ttt.value = value[value.length - 1]
    }
    selectedCategory.value = value.join('>');

}

const selectedCategory = ref("null");




provide('selectedCategory.value', selectedCategory);


const options = useFetch('/api/santab', { method: 'GET' }).data

</script>

<template>
    <div id="home">
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
            <el-form-item label="2. 选择商品类目" prop="resource">
                <el-cascader class="search" v-model="value" :options="options" :props="props" @change="handleChange"
                    placeholder="类目搜索，可输入关键词搜索类目" :clearable="true" size="large" filterable v-if="options" />
            </el-form-item>
            <el-text v-if="ttt !== 'null'">{{ ttt }}</el-text>
        </el-form>

    </div>
    <Photo />

</template>


<style>
h4 {
    text-align: center;
}

.search {
    width: 60%;
}

body {
    background-color: #f4f4f4;
}

#home {
    width: 90%;
    margin: 0 auto;
}
</style>