<template>
  <div class="LgFromItem">
    <label>{{ label }}</label>
    <div>
      <slot></slot>
      <div v-if="errorMsg" style="color: red">{{ errorMsg }}</div>
    </div>
  </div>
</template>

<script>
import AsyncValidator from "async-validator";
export default {
  name: "LgFromItem",
  props: {
    label: {
      type: String,
    },
    prop: {
      type: String,
    },
  },
  inject: ["form"],
  data() {
    return {
      errorMsg: "",
    };
  },
  mounted() {
    // console.log("itemVueObject:", this);
    this.$on("validate", () => {
      this.validate();
    });
  },
  methods: {
    validate() {
      console.log("item validte");
      if (!this.prop) return;
      const value = this.form.model[this.prop];
      const rule = this.form.rules[this.prop];
      const validator = new AsyncValidator({
        [this.prop]: rule,
      });
      return validator.validate({ [this.prop]: value }, (errors) => {
        if (errors) {
          this.errorMsg = errors[0].message;
        } else {
          this.errorMsg = "";
        }
      });
    },
  },
};
</script>
<style lang='less' scoped>
</style>
