<template>
  <div>
    <h1>App</h1>
    <hr>
    <my-table :data="goodslist">
      <template #header>
        <th>#</th>
        <th>商品名称</th>
        <th>价格</th>
        <th>标签</th>
        <th>操作</th>
      </template>
      <template #body="{row, index}">
        <td>{{index + 1}}</td>
        <td>{{row.goods_name}}</td>
        <td>￥{{row.goods_price}}</td>
        <td>
          <input type="text" class="form-control form-control-sm form-ipt" v-if="row.inputVisible" v-focus
            v-model.trim="row.inputValue" @blur="onInputConfirm(row)" @keyup.enter="onInputConfirm(row)"
            @keyup.esc="row.inputValue=''">
          <button type="button" class="btn btn-primary btn-sm" v-else @click="row.inputVisible = true">+Tag</button>
          <!-- 循环渲染标签信息 -->
          <span class="badge bg-warning text-dark ms-2" v-for="item in row.tags" :key="item">{{item}}</span>
        </td>
        <td>
          <button type="button" class="btn btn-danger btn-sm" @click="onRemove(row.id)">删除</button>
        </td>
      </template>
    </my-table>
  </div>
</template>

<script>
  import MyTable from './components/my-table/MyTable.vue'
  export default {
    name: "App",
    components: {
      MyTable,
    },
    data() {
        return {
            goodslist: []
        };
    },
    created() {
        this.getGoodsList();
    },
    methods: {
      // 请求商品数据列表
      async getGoodsList() {
          const { data: res } = await this.$http.get("/api/goods");
          // console.log(res)
          if (res.status !== 0)
              return console.log("获取列表失败！");
          this.goodslist = res.data;
      },
      // 删除功能
      onRemove(id) {
        this.goodslist = this.goodslist.filter( x => x.id !== id)
      },
      // 添加 tags 功能
      onInputConfirm(item) {
        const val = item.inputValue 
        item.inputValue = ''
        item.inputVisible = false
        if(!val || item.tags.indexOf(val) !== -1) return 
        item.tags.push(val)
      }
    },
    directives: {
      focus(el) {
        el.focus()
      }
    },
    components: { MyTable }
}
</script>

<style lang="less" scoped>
.form-ipt {
  width: 80px;
  display: inline;
}
</style>