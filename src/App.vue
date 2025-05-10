<script setup>
import { ref } from "vue";
import loginConf from "./conf/login.js";
import registerConf from "./conf/register.js";
import DynamicForm from "./components/DynamicForm.vue";
const registerRef = ref(null);
const loginRef = ref(null);
const onSubmit = (data) => {
  console.log("data", data);
};
const showLoginData = () => {
  const res = loginRef.value.getFormData();
  console.log("loginData", res);
};
const showRegisterData = () => {
  const res = registerRef.value.getFormData();
  console.log("registerData", res);
};
</script>

<template>
  <div>
    <DynamicForm
      ref="registerRef"
      :conf="registerConf"
      @submit="onSubmit"
    ></DynamicForm>
    <button @click="showRegisterData">注册</button>
    <DynamicForm
      ref="loginRef"
      :conf="loginConf"
      @submit="onSubmit"
    ></DynamicForm>
    <button @click="showLoginData">登录</button>
  </div>
</template>

<style scoped>
</style>
