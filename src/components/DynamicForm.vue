<template>
  <div>
    <render />
  </div>
</template>

<script setup>
import { ElCol, ElForm, ElFormItem, ElInput, ElRow } from "element-plus";
import { h, onMounted, reactive } from "vue";

const props = defineProps({
  conf: {
    required: true,
    type: Object,
  },
});
const form = reactive({});
onMounted(() => {
  props.conf.formItems.forEach((rows) => {
    rows.forEach((item) => {
      form[item.key] = item.value; // reactive 对象会自动处理响应式
    });
  });
});
const renderItem = (item) => {
  switch (item.type) {
    case "input":
      return h(ElInput, {
        ...item.attrs,
        modelValue: form[item.key],
        onInput: (val) => (form[item.key] = val),
      });
  }
};
const renderColumn = (columns) => {
  return columns.map((column) => {
    return h(
      ElCol,
      {
        span: column.colspan,
      },
      h(ElFormItem, { label: column.label }, () => renderItem(column))
    );
  });
};
const getFormData = () => form;
const renderRows = (rows) => {
  return rows.map((row) => {
    return h(ElRow, renderColumn(row));
  });
};
const render = () => {
  const { title, formItems } = props.conf;
  return h("div", [
    h("h1", title),
    h(ElForm, { "label-width": "120px" }, () => renderRows(formItems)),
  ]);
};
defineExpose({
  getFormData,
});
</script>

<style lang="scss" scoped>
</style>