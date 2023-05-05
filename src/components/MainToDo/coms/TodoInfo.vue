<template>
  <!-- TodoInfo组件 -->
  <div class="todo-info">
    <!-- 显示未完成的任务数量 -->
    <span class="total">{{ total }} item left</span>
    <!-- 任务状态选项卡 -->
    <div class="tab">
      <!-- 循环渲染任务状态选项 -->
      <a :class="[state===item?'active':'']" v-for="(item,index) in states" :key="index"
         @click="toggleState(item)">{{ item }}</a>
    </div>
    <!-- 清除已完成任务按钮 -->
    <el-button size="small" @click="clearCompleted">Clear Completed</el-button>
  </div>
</template>

<script>
export default {
  name: 'TodoInfo',
  props: {
    // 接收父组件传递的未完成任务数量
    total: Number
  },
  data() {
    return {
      // 任务状态选项
      states: ['all', 'active', 'completed'],
      // 当前选中的任务状态
      state: 'all'
    }
  },
  methods: {
    // 切换任务状态
    toggleState(state) {
      this.state = state
      // 向父组件发送事件，通知任务状态已改变
      this.$emit('toggleState', state)
    },
    // 清除已完成任务
    clearCompleted() {
      // 向父组件发送事件，通知清除已完成任务
      this.$emit('clearCompleted')
    }
  }
}
</script>

<style scoped>
.todo-info {
  display: flex;
  justify-content: space-between;
  padding: 5px 15px;
  font-weight: 400;
  line-height: 40px;
  border-top: 1px solid rgb(131, 175, 155);
}

.total {
  color: rgb(95, 108, 183);
}

.tab {
  /*display: flex;*/
  justify-content: space-between;
  width: 250px;
}

a {
  padding: 0 10px;
  border: 1px solid rgb(148, 158, 225);
  border-radius: 5px;
  margin: 8px;
}

a:active {
  background-color: rgb(95, 127, 255);
  color: #fff;
  cursor: pointer;
}

.clear {
  padding: 0 10px;
  background-color: rgb(17, 0, 171);
  border-radius: 5px;
  color: #fff;
  appearance: none;
  border: none;
  outline: none;
}

.el-button {
  appearance: none;
  border: none;
  outline: none;
  cursor: pointer;
  color: #666;
  position: relative;
  font-size: 17px;
  background-color: #A2A9EC;
  border-color: #A2A9EC;
  border-radius:15px;
}

</style>
