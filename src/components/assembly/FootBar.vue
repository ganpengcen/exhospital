<template>
  <div class="footBar">
   © 2019 - 我的应用程序
  </div>
</template>

<script>
    export default {
        name: "FootBar"
    }
</script>

<style scoped>
  .footBar{
    position: absolute;
    bottom: 0;
    border-top: 1px solid #e4eaec;;
    height: 39px;
    line-height: 40px;
    padding: 10px 40px;
    background: #f5f7fa;
    z-index: 3;
    text-align: left;
  }
</style>
