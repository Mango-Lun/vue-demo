<template>
  <div class="goods-container">
    <!-- 左侧图片区域 -->
    <div class="left">
      <div class="form-check">
        <input class="form-check-input" type="checkbox" value="" :id="id" :checked="checked" @change="onCheckBoxChange">
        <label class="form-check-label" :for="id">
          <img :src="thumb" alt="商品图片" class="thumb">
        </label>
      </div>
    </div>
    <!-- 右侧信息区域 -->
    <div class="right">
      <!-- 商品名称 -->
      <div class="top">{{title}}</div>
      <div class="bottom">
        <!-- 商品价格 -->
        <div class="price">￥{{price.toFixed(2)}}</div>
        <!-- 商品数量 -->
        <!-- <div class="count">数量:{{count}}</div> -->
        <es-counter :num="count" :min="1" @numChange="getNum"></es-counter>
      </div>
    </div>
  </div>
</template>

<script>
  import EsCounter from '../es-counter/EsCounter.vue'

  export default {
    name: 'EsGood',
    components: {
      EsCounter,
    },
    props: {
      // 唯一 key
      id: {
        type: [Number, String],
        required: true
      },
      thumb: {
        type: String,
        required: true
      },
      title: {
        type: String,
        required: true
      },
      price: {
        type: Number,
        required: true
      },
      count: {
        type: Number,
        required: true
      },
      checked: {
        type: Boolean,
        required: true
      }
    },
    emits: ['stateChange', 'countChange'],
    methods: {
      onCheckBoxChange(e) {
        // console.log(e.target.checked);
        this.$emit('stateChange', {
          id: this.id,
          value: e.target.checked
        })
      },
      getNum(num) {
        this.$emit('countChange', {
          id: this.id,
          value: num
        })
      }
    }
  }
</script>

<style lang="less" scoped>
.goods-container {
  display: flex;
  padding: 10px;

  +.goods-container {
    border-top: 1px solid #efefef;
  }

  // 左侧图片
  .left {
    margin-right: 10px;

    // 商品图片
    .thumb {
      display: block;
      width: 100px;
      height: 100px;
      background: #efefef;
    }
  }

  // 右侧商品信息
  .right {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;

    .top {
      font-weight: bold;
    }

    .bottom {
      display: flex;
      justify-content: space-between;
      align-items: center;

      .price {
        color: red;
        font-weight: bold;
      }
    }
  }
}

.form-check-input {
  margin-top: 3.4rem;
}
</style>