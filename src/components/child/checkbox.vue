/*
 * @Author: shaohaibin 
 * @Date: 2020-06-08 15:01:52 
 * @Last Modified by: shaohaibin
 * @Last Modified time: 2020-06-08 17:37:05
 */
<template>
  <div class="checkbox">
    <div class="checkbox_list" v-for="(item,index) in list" :key="index">
      <input
        type="checkbox"
        @change="change"
        :value="item.value"
        :id="item.id"
        v-model="checkValues"
        :disabled="isDisabled"
      />
      <label :for="item.id" :class="{'check-box':true,'disabled':isDisabled}"></label>
      <p>{{item.label}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      checkValues: this.defaultSelect
    }
  },
  props: {
    defaultSelect: {
      type: Array,
      default: () => {
        return []
      }
    },
    list: {
      type: Array,
      default: () => {
        return []
      }
    },
    isDisabled: {
      type: Boolean,
      default: false
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
      this.$emit('selectCheck', this.checkValues)
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
.checkbox_list {
  display: inline-block;
  margin-right: 10px;
}

@keyframes dothabottomcheck {
  0% {
    height: 0;
  }

  100% {
    height: 10px;
  }
}

@keyframes dothabottomcheck {
  0% {
    height: 0;
  }

  100% {
    height: 10px;
  }
}

@keyframes dothabottomcheck {
  0% {
    height: 0;
  }

  100% {
    height: 10px;
  }
}

@keyframes dothatopcheck {
  0% {
    height: 0;
  }

  50% {
    height: 0;
  }

  100% {
    height: 18px;
  }
}

@keyframes dothatopcheck {
  0% {
    height: 0;
  }

  50% {
    height: 0;
  }

  100% {
    height: 18px;
  }
}

@keyframes dothatopcheck {
  0% {
    height: 0;
  }

  50% {
    height: 0;
  }

  100% {
    height: 18px;
  }
}

input[type=checkbox] {
  display: none;
}

.check-box {
  height: 24px;
  width: 24px;
  background-color: #19579D;
  border-radius: 5px;
  position: relative;
  display: inline-block;
  -moz-transition: border-color ease 0.2s;
  -o-transition: border-color ease 0.2s;
  -webkit-transition: border-color ease 0.2s;
  transition: border-color ease 0.2s;
  cursor: pointer;
}

.checkbox p {
  width: auto;
  vertical-align: top;
  display: inline-block;
  font-size: 14px;
  margin 0
  padding 0
  margin-left 4px
}

.disabled {
  background: #F2F2F2;
}

.check-box::before, .check-box::after {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  position: absolute;
  height: 0;
  width: 3px;
  background-color: #fff;
  display: inline-block;
  -moz-transform-origin: left top;
  -ms-transform-origin: left top;
  -o-transform-origin: left top;
  -webkit-transform-origin: left top;
  transform-origin: left top;
  border-radius: 5px;
  content: ' ';
  -webkit-transition: opacity ease 0.5;
  -moz-transition: opacity ease 0.5;
  transition: opacity ease 0.5;
}

.check-box::before {
  top: 20px;
  left: 12px;
  -moz-transform: rotate(-150deg);
  -ms-transform: rotate(-150deg);
  -o-transform: rotate(-150deg);
  -webkit-transform: rotate(-150deg);
  transform: rotate(-150deg);
}

.check-box::after {
  top: 12px;
  left: 3px;
  -moz-transform: rotate(-45deg);
  -ms-transform: rotate(-45deg);
  -o-transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}

input[type=checkbox]:checked + .check-box, .check-box.checked {
  border-color: #34b93d;
}

input[type=checkbox]:checked + .check-box::after, .check-box.checked::after {
  height: 50px;
  -moz-animation: dothabottomcheck 0.2s ease 0s forwards;
  -o-animation: dothabottomcheck 0.2s ease 0s forwards;
  -webkit-animation: dothabottomcheck 0.2s ease 0s forwards;
  animation: dothabottomcheck 0.2s ease 0s forwards;
}

input[type=checkbox]:checked + .check-box::before, .check-box.checked::before {
  height: 120px;
  -moz-animation: dothatopcheck 0.4s ease 0s forwards;
  -o-animation: dothatopcheck 0.4s ease 0s forwards;
  -webkit-animation: dothatopcheck 0.4s ease 0s forwards;
  animation: dothatopcheck 0.4s ease 0s forwards;
}
</style>