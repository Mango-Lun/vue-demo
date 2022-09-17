<template>
  <div>
    <ul class="list-group">
      <!-- 列表组 -->
      <li class="list-group-item d-flex justify-content-between align-items-center" v-for="item in list" :key="item.id">
        <!-- 复选框 -->
        <input class="form-check-input" type="checkbox" value="" :id="item.id" v-model="item.done">
        <!-- 注意：App父组件通过 props 传递过来的 list 是引用类型的数据 -->
        <!-- 这里 v-model 双向绑定的结果是：用户的操作修改的是 App 组件中数据的状态 -->
        <label class="form-check-label" :for="item.id" :class="item.done ? 'delete' : ''">
          {{item.task}}
        </label>
        <!-- 徽标 -->
        <span class="badge bg-success rounded-pill" v-if="item.done">完成</span>
        <span class="badge bg-warning rounded-pill" v-else>未完成</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    list: {
      type: Array,
      required: true,
      default: [],
    },
  },
}
</script>

<style lang="less" scoped>
.list-group {
  width: 400px;
}

.delete {
  text-decoration: line-through;
  color: gray;
  font-style: italic;
}
</style>