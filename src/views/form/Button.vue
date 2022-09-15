<template>
  <div class="LgButton">
    <button @click="hanlder">
      <slot></slot>
    </button>
  </div>
</template>

<script>
export default {
  name: "LgButton",
  data() {
    return {};
  },
  components: {},
  created() {},
  mounted() {},
  methods: {
    hanlder(event) {
      event.preventDefault();
      this.$emit("click");
    },
  },
};
</script>
<style lang='less' scoped>
</style>
