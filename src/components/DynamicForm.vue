<template>
  <div><render /></div>
</template>

<script setup>
import { h } from "vue";

const props = defineProps({
  conf: {
    required: true,
    type: Object,
  },
});

const render = () => {
  const { title, formItems } = props.conf;
  return h("div", title);
};
</script>

<style lang="scss" scoped>
</style>