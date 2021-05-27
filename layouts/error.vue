<template>
  <div class="container">
    <h1 v-if="error.statusCode === 404">页面不存在</h1>
    <h1 v-else>应用发生错误异常</h1>
    <n-link to="/">
      <el-button type="primry" plain> 返回首页 </el-button>
    </n-link>
  </div>
</template>

<script>
export default {
  name: 'Error',
  props: ['error'],
}
</script>

<style scoped lang="scss">
.container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  h1 {
    margin-bottom: 2rem;
  }
}
</style>
