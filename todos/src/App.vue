<template>
  <div>
    <h1>App 根组件</h1>
  </div>
  <hr>
  <todo-input @add="onAddNewTask" style="width: 356px"></todo-input>
  <todo-list :list="tasklist" class="mt-2"></todo-list>
  <todo-button v-model:active="defaultActive"></todo-button>
</template>

<script>
// 导入 TodoList 组件
import TodoList from './components/todo-list/TodoList.vue'
// 导入 TodoInput 组件
import TodoInput from './components/todo-input/TodoInput.vue'
// 导入 TodoButton 组件
import TodoButton from './components/todo-button/TodoButton.vue'

export default {
  name: 'MyApp',
  data() {
    return {
      // 任务列表数组
      todolist: [
        { id: 1, task: '周一早晨9点开会', done: false },
        { id: 2, task: '周一晚上8点聚餐', done: false },
        { id: 3, task: '准备周三上午的演讲稿', done: true },
      ],
      // 下一个可用的 Id
      nextId: 4,
      // 默认完成状态
      defaultActive: 0
    }
  },
  computed: {
    tasklist(){
      switch(this.defaultActive) {
        case 0: // 全部
          return this.todolist
        case 1: // 已完成
          return this.todolist.filter(x => x.done === true)
        case 2: // 未完成
        return this.todolist.filter(x => x.done !== true)
      }
    }
  },
  methods:{
    onAddNewTask(x) {
      this.todolist.push({
        id: this.nextId,
        task: x,
        done: false, // 默认未完成
      })
      // id 自增1
      this.nextId++
    },
  },
  components: {
    TodoList,
    TodoInput,
    TodoButton,
  },
}
</script>

<style lang="less" scoped>

</style>