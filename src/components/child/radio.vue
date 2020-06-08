/*
 * @Author: shaohaibin 
 * @Date: 2020-06-08 10:09:24 
 * @Last Modified by: shaohaibin
 * @Last Modified time: 2020-06-08 17:39:18
 */

<template>
  <div>
    <div class="radio-check" v-for="(item,index) in list" :key="index">
      <input
        @change="change"
        :value="item.value"
        v-model="pickValue"
        type="radio"
        :name="item.name"
        :id="item.id"
        :disabled="isDisabled"
      />
      <label :for="item.id" class>
        <p>{{item.label}}</p>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pickValue: this.picked
    }
  },
  props: {
    picked: {
      type:String,
      default:""
    }, //默认选中的值
    list: {
      type: Array,
      default: () => {
        return []
      }
    },
    isDisabled:{
      type:Boolean,
      default:false
    }
  },
  watch: {
    list: {
      handler(val) {
        if (val && val.length > 0) {
          val.map(item => {
            if (!item.id) {
              return (item.id = this.uuid())
            }
          })
        }
      },
      immediate: true,
      deep: true
    }
  },
  methods: {
    change() {
      this.$emit('selectRadio', this.pickValue)
    },
    uuid() {
      var s = []
      var hexDigits = '0123456789abcdef'
      for (var i = 0; i < 36; i++) {
        s[i] = hexDigits.substr(Math.floor(Math.random() * 0x10), 1)
      }
      s[14] = '4' // bits 12-15 of the time_hi_and_version field to 0010
      s[19] = hexDigits.substr((s[19] & 0x3) | 0x8, 1) // bits 6-7 of the clock_seq_hi_and_reserved to 01
      s[8] = s[13] = s[18] = s[23] = '-'
      var uuid = s.join('')
      return uuid
    }
  }
}
</script>


<style lang="stylus" scoped>
.radio-check {
  position: relative;
  height: 35px;
  margin-right 20px
  display: inline-block;
  padding-left: 20px;
  white-space: nowrap;
}
.radio-check p {
  margin 0
  padding 0
}
.radio-check:nth-child(1){
  padding-left 0!important;
}

.radio-check > input {
  position: absolute;
  left: 0;
  top: 0;
  width: 20px;
  height: 20px;
  opacity: 0;
  display: inline-block;
}

.radio-check > label {
  position: relative;
  left: 30px;
  line-height: 20px;
  top: 0px;
  display: inline-block;
}

.radio-check > label:before {
  content: '';
  position: absolute;
  left: -30px;
  top: 0px;
  display: inline-block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 1px solid #19579D;
  transition: all 0.3s ease;
  -webkit-transition: all 0.3s ease;
  -moz-transition: all 0.3s ease;
}

.radio-check > label:after {
  content: '';
  position: absolute;
  left: -30px;
  top: 0px;
  display: inline-block;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  margin-top: 6px;
  margin-left: 6px;
  transition: all 0.3s ease;
  -webkit-transition: all 0.3s ease;
  -moz-transition: all 0.3s ease;
}

.radio-check input[type='radio']:checked + label:before {
  border-color: #19579D;
}

.radio-check input[type='radio']:checked + label:after {
  background: #19579D;
}
</style>