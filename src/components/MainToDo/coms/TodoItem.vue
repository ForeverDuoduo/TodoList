
<template>
  <!-- todo项的模板 -->
  <div :class="['todo-item',todo.completed?'completed':'']">

    <input type="checkbox" v-model="todo.completed">
    <label for="">{{ todo.content }}</label>
    <el-button round size="small" @click="delItem" type="primary">del</el-button>

  </div>
</template>

<script>
export default {
  name: 'TodoItem',

  props: {
    todo: Object
  },
  data() {
    return {
      isDisabled: false,
      isActiveDrawer: false
    }
  },
  methods: {
    // 删除todo项
    delItem() {
      this.isDisabled = true
      this.$emit('del', this.todo.id)
      localStorage.setItem('buttonStatus', JSON.stringify(this.isDisabled)) // 使用本地存储保存按钮状态
    },
    // 唤出右侧详细信息
    callDrawer() {
      this.isActiveDrawer = true
      this.$emit('click', this.todo.id)
    }
  }
}

</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: start;
  padding: 10px;
  font-size: 24px;
  color: #666;
  border-top: 1px solid rgba(0, 0, 0, .1);
}

/* 鼠标悬停在删除按钮上时，显示x */
/*.todo-item:hover el-button::after{*/
/*    position: relative;*/
/*    content:'xxx';*/
/*    font-size:20px;*/
/*    color:rgb(95, 127, 255);*/
/*}*/

/* 已完成的todo项添加删除线 */
.completed::after {
  content: '';
  color: #d9d9d9;
  text-decoration: line-through;
}

/* todo项的checkbox样式 */
input {
  width: 50px;
  height: 30px;
  /* appearance: none; */
  text-align: center;
  border: none;
  outline: none;
  display: block;
  border-radius: 50%;
}

/* todo项的内容样式 */
label {
  flex: 1; /*让它占据剩余的空间*/
  transition: color 0.4s;

}

/* 删除按钮样式 */
.el-button {
  appearance: none;
  border: none;
  outline: none;
  cursor: pointer;
  color: #666;
  position: relative;
  font-size: 17px;
  background-color: rgba(162, 169, 236, 0.5);
  border-color: #A2A9EC;
}

/* input:active{
    color:#d9d9d9;
    text-decoration: line-through;
} */
</style>

