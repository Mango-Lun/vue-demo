<template>
  <!-- form 表单 -->
  <form class="form-inline" @submit.prevent="onFormSubmit">
    <div class="input-group mb-2 mr-sm-2">
      <!-- 输入框前缀 -->
      <div class="input-group-prepend">
        <span class="input-group-text">任务</span>
      </div>
      <!-- 文本输入框 -->
      <input type="text" class="form-control" placeholder="请填写任务信息" v-model.trim="taskname">
    </div>
    <button type="submit" class="btn btn-primary mb-2">添加新任务</button>
  </form>
</template>

<script>
  export default {
    name: 'TodoInput',
    data() {
      return {
        // 新任务名称
        taskname: ''
      }
    },
    methods: {
      onFormSubmit() {
        if(!this.taskname) return alert('任务名称不能为空！')
        // 触发自定义事件，并向外传递参数
        this.$emit('add', this.taskname)
        // 传递完成，清空文本框
        this.taskname = ''
      }
    },
    emits: ['add']
  }
</script>

<style lang="less" scoped>

</style>