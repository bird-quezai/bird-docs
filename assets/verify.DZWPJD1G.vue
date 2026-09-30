<template>
  <div class="verify-demo">
    <h1>Verify 滑块验证组件示例</h1>
    <p>BiVerifySlide 组件是拼图滑块验证组件，支持嵌入模式（base）和弹框模式（dialog）。需要配合后端 captcha 验证码服务接口使用。</p>

    <!-- 组件说明 -->
    <div class="example-section">
      <h2>组件说明</h2>
      <div class="desc-content">
        <p>滑块验证组件需要配合后端 captcha 验证码服务使用。组件内部使用 AES 加密坐标信息，调用后端 <code>onGet</code> 获取拼图图片，调用 <code>onCheck</code> 验证坐标是否正确。</p>
        <div class="tag-row">
          <el-tag type="warning">需要后端接口</el-tag>
          <el-tag type="info">支持 base / dialog 两种模式</el-tag>
        </div>
      </div>
    </div>

    <!-- 嵌入模式 -->
    <div class="example-section">
      <h2>嵌入模式 (base)</h2>
      <p>组件直接嵌入页面中显示。</p>
      <div class="demo-wrapper">
        <div class="mock-verify-box">
          <div class="mock-verify-header">请完成安全验证</div>
          <div class="mock-verify-body">
            <div class="mock-puzzle-img">
              <div class="mock-puzzle-shape"></div>
            </div>
          </div>
          <div class="mock-verify-bar">
            <div class="mock-bar-placeholder">请拖动滑块完成拼图</div>
            <div class="mock-bar-block">➡️</div>
          </div>
        </div>
        <p class="mock-tip">⬆️ 上图为模拟展示，实际使用需接入后端 captcha 服务</p>
      </div>
    </div>

    <!-- 弹框模式 -->
    <div class="example-section">
      <h2>弹框模式 (dialog)</h2>
      <p>点击按钮后以弹框形式显示验证组件。</p>
      <el-button type="primary" @click="dialogVisible = true">打开滑块验证弹框</el-button>
      <el-dialog v-model="dialogVisible" title="安全验证" width="420px" :show-close="false">
        <div class="mock-verify-box">
          <div class="mock-verify-body">
            <div class="mock-puzzle-img">
              <div class="mock-puzzle-shape"></div>
            </div>
          </div>
          <div class="mock-verify-bar">
            <div class="mock-bar-placeholder">请拖动滑块完成拼图</div>
            <div class="mock-bar-block">➡️</div>
          </div>
        </div>
        <template #footer>
          <el-button @click="dialogVisible = false">取消</el-button>
        </template>
      </el-dialog>
    </div>

    <!-- 使用代码示例 -->
    <div class="example-section">
      <h2>使用示例代码</h2>
      <pre class="code-block">
import { BiVerifySlide } from '@bird/components';

// 嵌入模式
&lt;BiVerifySlide
  mode="base"
  :on-get="onGetCaptcha"
  :on-check="onCheckCaptcha"
  @success="handleVerifySuccess"
  @close="handleVerifyClose"
/&gt;

// 弹框模式
&lt;BiVerifySlide
  mode="dialog"
  :on-get="onGetCaptcha"
  :on-check="onCheckCaptcha"
  @success="handleVerifySuccess"
/&gt;

// onGet 获取验证码图片
const onGetCaptcha = async ({ captchaType }) => {
  const res = await api.getCaptcha({ captchaType });
  return res.data;
};

// onCheck 验证滑块位置
const onCheckCaptcha = async (data) => {
  const res = await api.checkCaptcha(data);
  return res.data;
};

// 验证成功回调
const handleVerifySuccess = ({ captchaVerification }) => {
  console.log('验证成功:', captchaVerification);
};
      </pre>
    </div>

    <!-- Props 说明 -->
    <div class="example-section">
      <h2>Props 说明</h2>
      <el-table :data="propsTableData" border size="small">
        <el-table-column prop="name" label="属性" width="140" />
        <el-table-column prop="type" label="类型" width="160" />
        <el-table-column prop="default" label="默认值" width="120" />
        <el-table-column prop="desc" label="说明" />
      </el-table>
    </div>

    <!-- Events 说明 -->
    <div class="example-section">
      <h2>Events 说明</h2>
      <el-table :data="eventsTableData" border size="small">
        <el-table-column prop="name" label="事件" width="140" />
        <el-table-column prop="param" label="参数" width="200" />
        <el-table-column prop="desc" label="说明" />
      </el-table>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

/** 弹框演示可见性 */
const dialogVisible = ref(false);

/** Props 说明数据 */
const propsTableData = [
  { name: 'mode', type: "'base' | 'dialog'", default: "'base'", desc: '组件显示模式，base 嵌入页面，dialog 以弹框形式显示' },
  { name: 'onGet', type: 'Function', default: '-', desc: '获取验证码图片的回调，必须返回 { repCode, repData } 结构' },
  { name: 'onCheck', type: 'Function', default: '-', desc: '验证滑块位置的回调，必须返回 { repCode } 结构，repCode 为 "0000" 表示验证成功' },
];

/** Events 说明数据 */
const eventsTableData = [
  { name: 'success', param: '{ captchaVerification }', desc: '验证成功时触发，参数包含加密后的验证码凭证' },
  { name: 'close', param: '-', desc: '关闭验证组件时触发' },
];
</script>

<style scoped>
.verify-demo {
  padding: 20px;
  max-width: 900px;
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
  margin-bottom: 15px;
  line-height: 1.6;
}

.tag-row {
  display: flex;
  gap: 8px;
}

code {
  background: #f0f0f0;
  padding: 2px 6px;
  border-radius: 3px;
  font-size: 12px;
  color: #d63384;
}

.code-block {
  background: #282c34;
  color: #abb2bf;
  padding: 16px;
  border-radius: 4px;
  font-family: 'Monaco', 'Menlo', monospace;
  font-size: 12px;
  overflow-x: auto;
  white-space: pre;
  line-height: 1.6;
}

.demo-wrapper {
  margin-top: 16px;
}

.mock-verify-box {
  max-width: 400px;
  margin: 0 auto;
  border: 1px solid #e4e7ed;
  border-radius: 4px;
  overflow: hidden;
}

.mock-verify-header {
  padding: 12px 16px;
  font-size: 16px;
  font-weight: 500;
  color: #1a1a1a;
  border-bottom: 1px solid #f0f0f0;
}

.mock-verify-body {
  position: relative;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  height: 160px;
}

.mock-puzzle-img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.mock-puzzle-shape {
  position: absolute;
  top: 40px;
  right: 60px;
  width: 50px;
  height: 50px;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 8px;
  border: 2px dashed #fff;
}

.mock-verify-bar {
  position: relative;
  height: 48px;
  margin-top: 10px;
  background: #f3f3f3;
}

.mock-bar-placeholder {
  position: absolute;
  top: 50%;
  left: 50%;
  color: #999;
  font-size: 14px;
  transform: translate(-50%, -50%);
}

.mock-bar-block {
  position: absolute;
  top: 4px;
  left: 4px;
  width: 54px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  background: #005ad9;
  color: #fff;
  border-radius: 4px;
}

.mock-tip {
  text-align: center;
  font-size: 12px;
  color: #999;
  margin-top: 12px;
}
</style>
