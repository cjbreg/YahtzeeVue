<template>
  <div class="  m-auto p-4 ">
    <div class="parrent items-center justify-center min-w-0 ">
      <LoginForm class="login" />
    </div>
  </div>
</template>

<script>
import LoginForm from "@/components/LoginFormComponent";
export default {
  components: {
    LoginForm,
  },
};
</script>

<style scoped>
.title {
  position: absolute;
  left: 10px;
  top: 10px;
}
.parrent {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 90vh;
}
.login {
  width: 100vw;
  max-width: 500px;
}
</style>
