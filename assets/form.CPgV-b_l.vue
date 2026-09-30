<template>
  <div class="form-demo">
    <h1>Form 组件示例</h1>
    <p>这是一个 Form 表单组件的示例页面，展示各种表单元素。</p>

    <!-- 基础输入框示例 -->
    <div class="example-section">
      <h2>基础输入框 (Input/Textarea)</h2>
      <BiJsonForm ref="inputFormRef" v-model="inputFormData" :columns="inputColumns" />
      <p>当前值: {{ JSON.stringify(inputFormData) }}</p>
      <div>
        <el-button type="primary" @click="handleInputSubmit">提交</el-button>
        <el-button @click="handleInputReset">重置</el-button>
      </div>
    </div>

    <!-- 数字输入框示例 -->
    <div class="example-section">
      <h2>数字输入框 (Number)</h2>
      <BiJsonForm ref="numberFormRef" v-model="numberFormData" :columns="numberColumns" />
      <p>当前值: {{ JSON.stringify(numberFormData) }}</p>
      <div>
        <el-button type="primary" @click="handleNumberSubmit">提交</el-button>
        <el-button @click="handleNumberReset">重置</el-button>
      </div>
    </div>

    <!-- 选择框示例 -->
    <div class="example-section">
      <h2>选择框 (Select/Radio)</h2>
      <BiJsonForm ref="selectFormRef" v-model="selectFormData" :columns="selectColumns" />
      <p>当前值: {{ JSON.stringify(selectFormData) }}</p>
      <div>
        <el-button type="primary" @click="handleSelectSubmit">提交</el-button>
        <el-button @click="handleSelectReset">重置</el-button>
      </div>
    </div>

    <!-- 日期选择示例 -->
    <div class="example-section">
      <h2>日期选择 (Date)</h2>
      <BiJsonForm ref="dateFormRef" v-model="dateFormData" :columns="dateColumns" />
      <p>当前值: {{ JSON.stringify(dateFormData) }}</p>
      <div>
        <el-button type="primary" @click="handleDateSubmit">提交</el-button>
        <el-button @click="handleDateReset">重置</el-button>
      </div>
    </div>

    <!-- 级联选择示例 -->
    <div class="example-section">
      <h2>级联选择 (Cascader)</h2>
      <BiJsonForm ref="cascaderFormRef" v-model="cascaderFormData" :columns="cascaderColumns" />
      <p>当前值: {{ JSON.stringify(cascaderFormData) }}</p>
      <div>
        <el-button type="primary" @click="handleCascaderSubmit">提交</el-button>
        <el-button @click="handleCascaderReset">重置</el-button>
      </div>
    </div>

    <!-- 开关示例 -->
    <div class="example-section">
      <h2>开关 (Switch)</h2>
      <BiJsonForm ref="switchFormRef" v-model="switchFormData" :columns="switchColumns" />
      <p>当前值: {{ JSON.stringify(switchFormData) }}</p>
      <div>
        <el-button type="primary" @click="handleSwitchSubmit">提交</el-button>
        <el-button @click="handleSwitchReset">重置</el-button>
      </div>
    </div>

    <!-- 综合示例 -->
    <div class="example-section">
      <h2>综合示例 (All Types)</h2>
      <BiJsonForm ref="allFormRef" v-model="allFormData" :columns="allColumns" />
      <p>当前值: {{ JSON.stringify(allFormData) }}</p>
      <div>
        <el-button type="primary" @click="handleAllSubmit">提交</el-button>
        <el-button @click="handleAllReset">重置</el-button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, useTemplateRef } from 'vue';
import { ElMessage } from 'element-plus';
import { BiJsonForm, type FormField } from '@bird/components/src';

// 基础输入框表单引用
const inputFormRef = useTemplateRef('inputFormRef');
// 数字输入框表单引用
const numberFormRef = useTemplateRef('numberFormRef');
// 选择框表单引用
const selectFormRef = useTemplateRef('selectFormRef');
// 日期选择表单引用
const dateFormRef = useTemplateRef('dateFormRef');
// 级联选择表单引用
const cascaderFormRef = useTemplateRef('cascaderFormRef');
// 开关表单引用
const switchFormRef = useTemplateRef('switchFormRef');
// 综合表单引用
const allFormRef = useTemplateRef('allFormRef');

// 基础输入框字段配置
const inputColumns: FormField[] = [
  {
    label: '用户名',
    prop: 'username',
    type: 'input',
    placeholder: '请输入用户名',
    defaultValue: 'admin',
  },
  {
    label: '密码',
    prop: 'password',
    type: 'password',
    placeholder: '请输入密码',
  },
  {
    label: '手机号',
    prop: 'phone',
    type: 'phone',
    placeholder: '请输入手机号',
  },
  {
    label: '邮箱',
    prop: 'email',
    type: 'email',
    placeholder: '请输入邮箱',
  },
  {
    label: '网站',
    prop: 'website',
    type: 'url',
    placeholder: '请输入网站地址',
  },
  {
    label: '描述',
    prop: 'description',
    type: 'textarea',
    placeholder: '请输入描述信息',
    compProps: { rows: 4 },
  },
];

// 基础输入框表单数据
let inputFormData = reactive({
  username: 'admin',
  phone: '13800138000',
  email: 'admin@example.com',
  website: 'https://example.com',
});

// 数字输入框字段配置
const numberColumns: FormField[] = [
  {
    label: '年龄',
    prop: 'age',
    type: 'number',
    placeholder: '请输入年龄',
    compProps: {
      min: 0,
      max: 120,
      step: 1,
    },
  },
  {
    label: '分数',
    prop: 'score',
    type: 'number',
    placeholder: '请输入分数',
    compProps: {
      min: 0,
      max: 100,
      step: 0.5,
    },
  },
  {
    label: '金额',
    prop: 'amount',
    type: 'number',
    placeholder: '请输入金额',
    compProps: {
      step: 0.01,
    },
  },
];

// 数字输入框表单数据
let numberFormData = reactive({
  age: 25,
  score: 95.5,
  amount: 100.5,
});

// 选择框字段配置
const selectColumns: FormField[] = [
  {
    label: '性别',
    prop: 'gender',
    type: 'select',
    options() {
      return [
        { label: '男', value: 'male' },
        { label: '女', value: 'female' },
      ];
    },
    defaultValue: 'male',
  },
  {
    label: '状态',
    prop: 'status',
    type: 'radio',
    options: [
      { label: '启用', value: 1 },
      { label: '禁用', value: 0 },
    ],
    defaultValue: 1,
  },
  {
    label: '爱好',
    prop: 'hobbies',
    type: 'select',
    options: [
      { label: '阅读', value: 'reading' },
      { label: '运动', value: 'sports' },
      { label: '音乐', value: 'music' },
      { label: '旅行', value: 'travel' },
    ],
    compProps: {
      multiple: true,
      placeholder: '请选择爱好',
    },
  },
];

// 选择框表单数据
let selectFormData = reactive({
  gender: 'male',
  status: 1,
  hobbies: ['reading', 'sports'],
});

// 日期选择字段配置
const dateColumns: FormField[] = [
  {
    label: '出生日期',
    prop: 'birthDate',
    type: 'date',
    placeholder: '请选择出生日期',
    compProps: {
      dateType: 'date',
    },
  },
  {
    label: '入职日期',
    prop: 'hireDate',
    type: 'date',
    placeholder: '请选择入职日期',
    compProps: {
      dateType: 'year',
    },
  },
  {
    label: '请假时间',
    prop: 'leaveTime',
    type: 'date',
    placeholder: '请选择请假时间范围',
    compProps: {
      dateType: 'daterange',
    },
  },
];

// 日期选择表单数据
let dateFormData = reactive({
  birthDate: '2000-01-01',
  hireDate: '2020',
  leaveTime: ['2025-01-01', '2025-01-10'],
});

// 级联选择字段配置
const cascaderColumns: FormField[] = [
  {
    label: '所在地区',
    prop: 'region',
    type: 'cascader',
    options: [
      {
        value: 'zhejiang',
        label: '浙江',
        children: [
          {
            value: 'hangzhou',
            label: '杭州',
            children: [
              { value: 'xihu', label: '西湖' },
              { value: 'binjiang', label: '滨江' },
            ],
          },
          {
            value: 'ningbo',
            label: '宁波',
            children: [
              { value: 'haishu', label: '海曙' },
              { value: 'jiangbei', label: '江北' },
            ],
          },
        ],
      },
      {
        value: 'jiangsu',
        label: '江苏',
        children: [
          {
            value: 'nanjing',
            label: '南京',
            children: [
              { value: 'zhonghua', label: '中华门' },
              { value: 'xuanwu', label: '玄武湖' },
            ],
          },
          {
            value: 'suzhou',
            label: '苏州',
            children: [
              { value: 'gusu', label: '姑苏' },
              { value: 'wuzhong', label: '吴中' },
            ],
          },
        ],
      },
    ],
    compProps: {
      props: {
        checkStrictly: false,
      },
    },
  },
];

// 级联选择表单数据
let cascaderFormData = reactive({
  region: ['zhejiang', 'hangzhou', 'xihu'],
});

// 开关字段配置
const switchColumns: FormField[] = [
  {
    label: '是否启用',
    prop: 'enabled',
    type: 'switch',
    defaultValue: 1,
  },
  {
    label: '邮件通知',
    prop: 'emailNotification',
    type: 'switch',
    compProps: {
      activeText: '开启',
      inactiveText: '关闭',
      activeValue: 'on',
      inactiveValue: 'off',
    },
    defaultValue: 'on',
  },
];

// 开关表单数据
let switchFormData = reactive({
  enabled: 1,
  emailNotification: 'on',
});

// 综合示例字段配置
const allColumns: FormField[] = [
  {
    label: '姓名',
    prop: 'name',
    type: 'input',
    placeholder: '请输入姓名',
  },
  {
    label: '年龄',
    prop: 'age',
    type: 'number',
    placeholder: '请输入年龄',
    compProps: { min: 0, max: 120 },
  },
  {
    label: '性别',
    prop: 'gender',
    type: 'select',
    options: [
      { label: '男', value: 'male' },
      { label: '女', value: 'female' },
    ],
  },
  {
    label: '部门',
    prop: 'department',
    type: 'radio',
    options: [
      { label: '技术部', value: 'tech' },
      { label: '销售部', value: 'sales' },
      { label: '市场部', value: 'marketing' },
    ],
  },
  {
    label: '入职日期',
    prop: 'hireDate',
    type: 'date',
    compProps: { dateType: 'date' },
  },
  {
    label: '所在地区',
    prop: 'region',
    type: 'cascader',
    options: [
      {
        value: 'zhejiang',
        label: '浙江',
        children: [
          { value: 'hangzhou', label: '杭州' },
          { value: 'ningbo', label: '宁波' },
        ],
      },
    ],
  },
  {
    label: '是否在职',
    prop: 'isActive',
    type: 'switch',
    defaultValue: 1,
  },
  {
    label: '个人简介',
    prop: 'bio',
    type: 'textarea',
    placeholder: '请输入个人简介',
    compProps: { rows: 3 },
  },
];

// 综合示例表单数据
let allFormData = reactive({
  name: '张三',
  age: 28,
  gender: 'male',
  department: 'tech',
  hireDate: '2022-03-15',
  region: ['zhejiang', 'hangzhou'],
  isActive: 1,
  bio: '这是一段个人简介...',
});

// 基础输入框处理函数
const handleInputSubmit = async () => {
  const data = await inputFormRef.value?.validate();
  setTimeout(() => {
    console.log('提交基础输入框表单', data);
    ElMessage.success('基础输入框表单提交成功');
  }, 1000);
};

const handleInputReset = () => {
  inputFormRef.value?.reset();
  ElMessage.success('基础输入框表单重置成功');
};

// 数字输入框处理函数
const handleNumberSubmit = async () => {
  const data = await numberFormRef.value?.validate();
  setTimeout(() => {
    console.log('提交数字输入框表单', data);
    ElMessage.success('数字输入框表单提交成功');
  }, 1000);
};

const handleNumberReset = () => {
  numberFormRef.value?.reset();
  ElMessage.success('数字输入框表单重置成功');
};

// 选择框处理函数
const handleSelectSubmit = async () => {
  const data = await selectFormRef.value?.validate();
  setTimeout(() => {
    console.log('提交选择框表单', data);
    ElMessage.success('选择框表单提交成功');
  }, 1000);
};

const handleSelectReset = () => {
  selectFormRef.value?.reset();
  ElMessage.success('选择框表单重置成功');
};

// 日期选择处理函数
const handleDateSubmit = async () => {
  const data = await dateFormRef.value?.validate();
  setTimeout(() => {
    console.log('提交日期选择表单', data);
    ElMessage.success('日期选择表单提交成功');
  }, 1000);
};

const handleDateReset = () => {
  dateFormRef.value?.reset();
  ElMessage.success('日期选择表单重置成功');
};

// 级联选择处理函数
const handleCascaderSubmit = async () => {
  const data = await cascaderFormRef.value?.validate();
  setTimeout(() => {
    console.log('提交级联选择表单', data);
    ElMessage.success('级联选择表单提交成功');
  }, 1000);
};

const handleCascaderReset = () => {
  cascaderFormRef.value?.reset();
  ElMessage.success('级联选择表单重置成功');
};

// 开关处理函数
const handleSwitchSubmit = async () => {
  const data = await switchFormRef.value?.validate();
  setTimeout(() => {
    console.log('提交开关表单', data);
    ElMessage.success('开关表单提交成功');
  }, 1000);
};

const handleSwitchReset = () => {
  switchFormRef.value?.reset();
  ElMessage.success('开关表单重置成功');
};

// 综合示例处理函数
const handleAllSubmit = async () => {
  const data = await allFormRef.value?.validate();
  setTimeout(() => {
    console.log('提交综合示例表单', data);
    ElMessage.success('综合示例表单提交成功');
  }, 1000);
};

const handleAllReset = () => {
  allFormRef.value?.reset();
  ElMessage.success('综合示例表单重置成功');
};
</script>

<style scoped>
.form-demo {
  padding: 20px;
}

.example-section {
  margin-bottom: 40px;
  padding: 20px;
  border: 1px solid #eee;
  border-radius: 8px;
}

h1 {
  color: #333;
  margin-bottom: 20px;
}

h2 {
  color: #555;
  margin-bottom: 15px;
}

p {
  margin-bottom: 10px;
  line-height: 1.6;
}
</style>
