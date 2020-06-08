<template>
  <div class="hello">
    <Radio @selectRadio="selectRadio" :isDisabled="false" :list="listRadio" :picked="selectSex"></Radio>
    <br />
    <Checkbox
      @selectCheck="selectCheck"
      :list="listCheckbox"
      :defaultSelect="defaultSelect"
      :isDisabled="false"
    ></Checkbox>
  </div>
</template>

<script>
import Checkbox from "./child/checkbox";
import Radio from "./child/radio";
export default {
  props: {
    msg: String
  },
  components: {
    Checkbox,
    Radio
  },
  data() {
    return {
      //radio 数据
      selectSex: "man", //默认选中radio项
      listRadio: [
        {
          label: "男",
          name: "sex",
          value: "man"
        },
        {
          label: "女",
          name: "sex",
          value: "woman"
        }
      ],
      //checkbox 数据
      defaultSelect: ["pear", "banana"], //默认选中checkbox项
      listCheckbox: [
        {
          label: "苹果",
          value: "apple"
        },
        {
          label: "桃子",
          value: "pear"
        },
        {
          label: "橘子",
          value: "orange"
        },
        {
          label: "香蕉",
          value: "banana"
        }
      ]
    };
  },
  methods: {
    selectRadio(val) {
      //获取radio选中项
      this.selectSex = val;
    },
    selectCheck(val) {
      //获取checkbox选中项
      this.defaultSelect = val;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
