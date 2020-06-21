
<template>
  <div>
    <input
      type="text"
      class="input"
      :style="styles"
      @input="input"
      v-model="inputVal"
      :placeholder="placeholder"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputVal: this.defaultValue,
      styles: {
        width: this.width + 'px',
        textAlign: this.align,
        border: this.border ? '1px solid #ddd' : 'none'
      }
    }
  },
  props: {
    defaultValue: {
      type: String | Number,
      default: ''
    },
    border: {
      type: Boolean,
      default: false
    },
    decimal: {
      type: String | Number,
      default: 2 //默认保留两位小数
    },
    numberType: {
      type: String,
      default: 'integer' //默认为整数类型
    },
    negative: {
      type: Boolean,
      default: false
    },
    width: {
      type: String | Number,
      default: 120
    },
    align: {
      type: String,
      default: 'left'
    },
    placeholder: {
      type: String,
      default: ''
    }
  },
  methods: {
    input(e) {
      let val = e.target.value
      let num = 3
      let res
      switch (this.numberType) {
        case 'integer':
          if (this.negative) {
            res = this.integerFun_negative(val)
          } else {
            res = this.integerFun(val)
          }
          break
        case 'float':
          if (this.negative) {
            res = this.toFiexed_negative(val, this.decimal)
          } else {
            res = this.toFiexed(val, this.decimal)
          }
          break
      }
      this.inputVal = res
      var reg = /^[0-9]/g
      let finalValue = reg.test(res) ? Number(res):res=='-'? 0 : res
      //如果输入值是以数字开头的那么将输入值转换为Number类型 12.===>12
      //如果不是并且只输入了一个-负号，那么默认设置为0 -===>0
      this.$emit('getInputVal', finalValue)
    },
    integerFun(val) {
      //正整数
      let res = val.replace(/[^0-9]/g, '').replace(/^(0\d)/, 0)
      return res
    },
    integerFun_negative(val) {
      //整数(包含正整数和负整数)
      let res = val
        .replace(/[^\d-]/g, '')
        .replace(/\-{2,}/g, '-')
        .replace('-', '$#$')
        .replace(/\-/g, '')
        .replace('$#$', '-')
        .replace(/^(\-0)/, '-') //限制负号-后面加0
        .replace(/^(0\d)/, 0) //限制0后面输入数字
        .replace(/^(\d+)(\-)/, '$1') //限制数字后面输入负号-
      return res
    },
    toFiexed(val, num) {
      //正浮点数
      //val 数字 num 保留几位小数
      let res = val
        .replace(/[^\d.]/g, '')
        .replace(/\.{2,}/g, '.')
        .replace('.', '$#$')
        .replace(/\./g, '')
        .replace('$#$', '.')
        //.replace(/^(\-)*(\d+)\.(\d{2}).*$/, '$1$2.$3')
        .replace(new RegExp(`^(\\-)*(\\d+)\\.(\\d{${num}}).*$`), '$1$2.$3')
        .replace(/^\./g, '')
        .replace(/^(0\d)/, 0)
      return res
    },
    toFiexed_negative(val, num) {
      //浮点数 (包含正浮点和负浮点数)
      let res = val
        .replace(/[^\d.-]/g, '') //开头只能是数字 . -
        //限制输入值只能有一个.
        .replace(/\.{2,}/g, '.')
        .replace('.', '$#$')
        .replace(/\./g, '')
        .replace('$#$', '.')
        //限制输入值只能有一个-
        .replace(/\-{2,}/g, '-')
        .replace('-', '$#$')
        .replace(/\-/g, '')
        .replace('$#$', '-')
        .replace(new RegExp(`^(\\-)*(\\d+)\\.(\\d{${num}}).*$`), '$1$2.$3')
        .replace(/^\./g, '')
        .replace(/^(0\d)/, 0)
        .replace(/^(\-0)/, '-') //限制负号-后面加0
        .replace(/^(\d+)(\-)/, '$1') //限制数字后面输入负号-
      return res
    }
  }
}
</script>


<style lang="stylus" scoped>
.input {
  padding: 0 4px;
}
</style>