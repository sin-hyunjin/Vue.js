<!-- Vue는 3부분으로 나눠짐 
     1. template
     2. script - javascript 로직이 들어감
     3. style
-->
<template>
  <!--일반함수와 똑같이 인자전달이 가능하다  -->
  <div class="name">{{ name }}</div>
  <div class="newName">{{ newName }}</div>
  <button class="btn btn-primary" v-on:click="updateName">Click</button>
</template>

<script>
import { ref, reactive } from "vue";
export default {
  setup() {
    // reactive 화면에서도 바뀌게 할려면 ref.value 값으로 접근해야한다
    // 배열이나 객체를 사용할떄는 reactive를 사용해야한다.
    let name = ref("Kossie Coder1");
    let newName = reactive({
      id: 1,
      name: "Hyun jin",
    });
    // const greeting = (name) => {
    //   return "Hello, " + name;
    // };
    const updateName = () => {
      newName.id = 2;
      name.value = "Kossie Coder";
      console.log(name);
    };

    // 원하는 변수들은 template에서 접근이 가능
    return {
      name,
      updateName,
      newName,

      // greeting,
    };
  },
};
</script>

<style>
.name {
  color: red;
}
</style>
