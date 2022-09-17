<template>
  <div>
    <div class="counter-container">
      <button type="button" class="btn btn-light btn-sm" @click="onSubClick">-</button>
      <input type="number" class="form-control form-control-sm ipt-num" v-model.lazy="this.number">
      <button type="button" class="btn btn-light btn-sm" @click="onAddClick">+</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'EsCounter',
    data() {
      return {
        number: this.num
      }
    },
    emits: ['numChange'],
    props: {
      num: {
        type: Number,
        default: 0
      },
      min: {
        type: Number,
        dafault: NaN
      }
    },
    methods: {
      onSubClick() {
        if(!isNaN(this.min) && this.number - 1 >= this.min)
        this.number --
      },
      onAddClick() {
        this.number ++
      }
    },
    watch: {
      number(newValue) {
        const parseResult = parseInt(newValue)
        if(isNaN(parseResult) || parseResult < 1){
          this.number = 1
          return
        }
        if(String(newValue).indexOf('.') !== -1) {
          this.number = parseResult
          return
        }
        // console.log(this.number);
        this.$emit('numChange', this.number)
      }
    }
  }
</script>

<style lang="less" scoped>
.counter-container {
  display: flex;

  .btn {
    width: 25px;
  }

  .ipt-num {
    width: 34px;
    text-align: center;
    margin: 0 4px;
  }
}
</style>