<template>
  <form>
    <slot></slot>
  </form>
</template>

<script>
export default {
  name: "LgForm",
  props: {
    model: {
      type: Object,
    },
    rules: {
      type: Object,
    },
  },
  provide() {
    return {
      form: this,
    };
  },
  data() {
    return {};
  },
  components: {},
  created() {},
  mounted() {},
  methods: {
    validate2(cb) {
      const tasks = this.$children
        .filter((child) => child.prop)
        .map((child) => child.validate());

      Promise.all(tasks)
        .then(() => cb(true))
        .catch(() => cb(false));
    },
    validate(cb) {
      const allValideteFn = this.$children
        .filter((item) => item.prop)
        .map((item) => item.validate());
      Promise.all(allValideteFn)
        .then(() => {
          cb(true);
        })
        .catch(() => {
          cb(false);
        });
    },
  },
};
</script>
<style lang='less' scoped>
</style>
