<!-- Vue는 3부분으로 나눠짐 
     1. template
     2. script - javascript 로직이 들어감
     3. style -
-->
<template>
  <div class="name">{{ name }}</div>
  <duv>123</duv>
</template>
<script>
export default {
  setup() {
    const name = "Kossie Coder";

    // 원하는 변수들은 template에서 접근이 가능
    return {
      name,
    };
  },
};
</script>
<style>
.name {
  color: red;
}
</style>
