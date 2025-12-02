<template>
  <div class="main">
    <h2>Todolist</h2>
    <form @submit.prevent>
      <input type="text" v-model="text"> <button @click="hairu">提交</button>
    </form>
    <div v-for="(item, index) in arr_0" :key="item.originIndex">
      <span :style="{textDecoration: item.del ? 'line-through' : 'none'}">{{ item.content }}</span> 
      <button @click="kae(index)">切换</button> <button @click="dlt(index)">删除</button>
    </div>
    <div class="btn">
      <button @click="zennbu" style="margin: 1;">全部</button>
      <button @click="kanse">已完成事项</button>
      <button @click="mikanse">未完成事项</button>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';

const text = ref('');
const arr = reactive([]);
const arr_0 = ref([])
let originIndex = 0

function hairu() {
  arr.push({
    content: text.value,
    del: false,
    originIndex: originIndex
});
  originIndex++;
  arr_0.value = [...arr];
}

function kae(index) {
  arr_0.value[index].del = !arr_0.value[index].del
}

function dlt(index) {
  const targetOriginIndex = arr_0.value[index].originIndex;
  const currentArrIndex = arr.findIndex(item => item.originIndex === targetOriginIndex);
  if (currentArrIndex !== -1) {
    arr.splice(currentArrIndex, 1);
  }
  arr_0.value.splice(index, 1);
}

function zennbu() {
  arr_0.value = [...arr]
}

function kanse() {
  arr_0.value = arr.filter((item) => {
    return item.del; 
  });
}

function mikanse() {
  arr_0.value = arr.filter((item) => {
    return !item.del; 
  });
}

</script>

<style>
body {
  padding: 0;
  margin: 0;
  height: 100vh;
  width: auto;
  background-color: rgb(203, 212, 230);
  display: flex;
  justify-content: center;
  align-items: center;
}

span {
  display: inline-block;
  margin: 4px 6px;
  /* 优化任务文本样式：增加字号和颜色，提升可读性 */
  font-size: 16px;
  color: #333;
  min-width: 20px; /* 固定文本宽度，让任务项对齐更整齐 */
}

.main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #fff;
  padding: 30px 40px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  max-width: 500px;
  width: 100%;
}

h2 {
  color: rgb(10, 10, 85); /* 和按钮背景色呼应，保持风格统一 */
  margin: 0 0 20px 0; /* 只保留下方间距，避免和内容区顶部紧贴 */
  font-size: 24px;
}

/* 优化表单样式：让 input 和提交按钮对齐更协调 */
form {
  width: 100%; /* 占满 .main 宽度，让 input 更宽 */
  margin-bottom: 10px; /* 和下方任务列表隔开 */
}

input {
  /* 匹配按钮高度和风格，增加内边距 */
  padding: 10px 12px;
  font-size: 15px;
  border: 2px solid #ddd;
  border-radius: 6px;
  width: calc(100% - 110px); /* 计算宽度，给提交按钮留空间 */
  margin-right: 8px; /* 和提交按钮隔开 */
  box-sizing: border-box; /* 避免 padding 撑大宽度 */
}

.btn {
  display: flex;
  gap: 20px; /* 增大按钮间距，解决拥挤（原 2px 改为 12px） */
  margin-top: 10px; /* 和上方任务列表隔开 */
  width: 100%;
}

button {
  font-size: 15px;
  border: none;
  background: rgb(10, 10, 85);
  color: rgb(228, 134, 12);
  border-radius: 6px; /* 增大圆角，更现代 */
  cursor: pointer;
  /* 新增：按钮内边距，让按钮更饱满（避免文字紧贴边框） */
  padding: 10px 18px;
  margin: 2px;
  /* 新增：过渡动画，hover 更流畅 */
  transition: all 0.2s ease;
}

/* 新增：按钮交互反馈，提升体验 */
button:hover {
  background: rgb(26, 26, 139); /* 加深背景色 */
  color: #fff; /* 文字变白，增强对比 */
  box-shadow: 0 2px 8px rgba(10, 10, 85, 0.2); /* 增加阴影，突出按钮 */
}

</style>
