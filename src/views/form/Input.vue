<template>
  <div class="LgInput">
    <input :type="type" :value="value" @input="handlerInput" v-bind="$attrs" />
    <!-- <input v-bind="$attrs" :type="type" :value="value" @input="handleInput" /> -->
  </div>
</template>

<script>
export default {
  name: "LgInput",
  inheritAttrs: false,
  props: {
    type: {
      type: String,
      default: "text",
    },
    value: {
      type: String,
    },
  },
  data() {
    return {};
  },

  methods: {
    handleInput() {
      console.log(222);
    },
    findPrarent(parent) {
      while (parent) {
        // console.log(parent);
        if (parent.name == "LgFromItem") {
          break;
        } else {
          parent = parent.$parent;
        }
      }
      return parent;
    },
    handlerInput(event) {
      console.log(1111);
      this.$emit("input", event.target.value);
      //   const parent = this.findPrarent(this.$parent);
      const parent = this.$parent;
      if (parent) {
        parent.$emit("validate");
        // parent.validate();
      }
    },
  },
};
</script>
<style lang='less' scoped>
</style>
