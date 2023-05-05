<template>
  <div class="main-todo">
    <input type="text" class="add-todo" placeholder="what to do?" autofocus v-model="content" @keyup.enter="addTodo">
    <div class="infinite-list" style="overflow-y:auto;max-height: 250px;">
      <todo-item v-for="(item,index) in filterData" :key="index" :todo="item" @del="handleDeleteItem"></todo-item>
    </div>
    <todo-info :total="total" @toggleState="handleToggleState" @clearCompleted="handleClear"></todo-info>
  </div>
</template>





<script>
import TodoItem from './coms/TodoItem.vue'
import TodoInfo from './coms/TodoInfo.vue'

let id = 0;
export default {
  name: 'MainToDo',
  data() {
    return {
      todoData: [],
      content: '',
      total: 0,
      filter: 'all'
    }
  },
  methods: {
    addTodo() {
      if (this.content === '') return
      this.todoData.unshift({
        id: id++,
        content: this.content,
        completed: false
      })
      this.content = ''
      localStorage.setItem('todoData', JSON.stringify(this.todoData))
    },
    handleDeleteItem(id) {
      this.todoData.splice(this.todoData.findIndex(item => item.id === id), 1)
      localStorage.setItem('todoData', JSON.stringify(this.todoData))
    },
    handleToggleState(state) {
      this.filter = state
      localStorage.setItem('filter', state)
    },
    handleClear() {
      this.todoData = this.todoData.filter(item => item.completed === false)
      localStorage.setItem('todoData', JSON.stringify(this.todoData))
    }
  },
  watch: {
    todoData: {
      deep: true,
      handler() {
        this.total = this.todoData.filter(item => item.completed === false).length
        localStorage.setItem('todoData', JSON.stringify(this.todoData))
      }
    }
  },
  computed: {
    filterData() {
      switch (this.filter) {
        case 'all':
          return this.todoData
        case 'active':
          return this.todoData.filter(item => item.completed === false)
        case 'completed':
          return this.todoData.filter(item => item.completed === true)
      }
    }
  },
  components: {
    TodoItem: TodoItem,
    TodoInfo: TodoInfo
  },
  mounted() {
    if (localStorage.getItem('todoData')) {
      try {
        this.todoData = JSON.parse(localStorage.getItem('todoData'))
        id = this.todoData[0].id + 1
      } catch (e) {
        localStorage.removeItem('todoData')
      }
    }
    if (localStorage.getItem('filter')) {
      try {
        this.filter = localStorage.getItem('filter')
      } catch (e) {
        localStorage.removeItem('filter')
      }
    }
  }
}
</script>

<style scoped>
.main-todo {
  margin: 0 auto;
  width: 600px;
  background-color: #fff;
  box-shadow: 0 0 25px #666;
  border-radius: 25px;
}

.add-todo {
  padding: 16px 16px 16px 36px;
  width: 100%;
  font-size: 24px;
  font-weight: inherit;
  font-family: inherit;
  color: inherit;
  border: none;
  outline: none;
  box-sizing: border-box;
  color: #666;
  border-radius: 25px;
}
</style>
