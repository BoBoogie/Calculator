<template>
  <div class="calculator-container">
    <input class="show" :value="screen">
    <div class="btn-row">
      <button class="btn" @click="clickHandler(item)" v-for="(item,index) in btnName" :key="index">
        {{ item }}
      </button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'CounterHome',
  data() {
    return {
      //按钮名称
      btnName: [
        '%', 'CE', 'C', 'del', '1/x', 'x^2', '√x', '÷', 7, 8, 9, '×', 4, 5, 6, '-', 1, 2, 3, '+', '+/-', 0, '.', '='
      ],
      //显示值
      value: '0' + '',
      operator: ['+', '-', '×', '÷','%'],
      screen:''
    }
  },
  methods: {
    //点击按钮事件
    clickHandler(item) {
      this.screen = this.value
      //点击数字按钮才执行拼接
      if (typeof item === "number" || this.operator.includes(item) === true && typeof this.value === "string") {
        //不能重复点击运算符
        if (this.operator.includes(this.value.slice(this.value.length - 1, this.value.length)) === true && this.operator.includes(item)) return;
        //首两位不能重复点击0
        if (this.value.slice(0, 2) === '0' && Number(item) === 0) return
        //去除首位0
        if (this.value.slice(0, 1) === '0' && this.value.slice(1, 2) !== '.') {
          this.value = this.value.slice(1)
        }
        //拼接
        this.value += item + ''
      }
      //点击数字以外的按钮
      switch (item) {
        case '.':
          //不能出现两个.
          if (this.value.slice(0, this.value.length).includes('.') === false) {
            this.value = this.value + '.'
          }
          break
        case 'del':
          this.value = '0'
          break
        case 'C':
          this.value = this.value.slice(0, this.value.length - 1)
          if (this.value === '') {
            this.value = '0'
          }
          break
        case '=':
          this.value = this.value.replace(/÷/g, '/')
          this.value = this.value.replace(/×/g, '*')
          this.value = eval(this.value)
          this.value += ''
          break
      }

    }
  }

}
</script>

<style lang="less" scoped>
.calculator-container {
  height: 625px;
  width: 485px;
  background-color: #202020;
  border-radius: 15px;
  border: 1px solid rgba(255, 255, 255, 0.15);
  margin: 100px auto;

  .show {
    background-color: #202020;;
    border-radius: 15px;
    border: 0;
    width: 100%;
    height: 105px;
    margin-top: 50px;
    padding: 0 20px;
    text-align: right;
    box-sizing: border-box;
    color: #ffffff;
    font-size: 60px;
  }

  .btn-row {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: stretch;

    .btn:hover {
      background-color: #3B3B3B;
    }

    .btn:active {
      background-color: #323232;
    }

    .btn:last-child {
      background-color: #E183D9;
      color: #000;
    }

    .btn:hover:last-child {
      background-color: rgba(225, 131, 217, 0.9)
    }

    .btn:active:last-child {
      background-color: rgba(225, 131, 217, 0.8)
    }

    .btn {
      width: 115px;
      height: 75px;
      margin: 1px;
      background-color: #323232;
      border-radius: 5px;
      font-size: 30px;
      color: #fff;
      line-height: 75px;
      cursor: pointer;
    }
  }
}


</style>
