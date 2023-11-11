### Vue3 학습

기본 : https://youtu.be/-tVaahsXpwk

Todolist : https://youtu.be/qhjxAP1hFuI

<hr/>

# Vue란?

> 사용자 인터페이스를 구축하기 위한 JavaScript 프레임워크

> 표준 HTML, CSS 및 JavaScript를 기반으로 하는 구축과 유사한 사용자 인터페이스를

> 개발하는 데 도움이 되며 선언 및 구성 요소 기반 프로그래밍 모델을 제공

### 프로그레시브 프레임워크

> - 빌드 단계 없이 정적 HTML 향상

> - 모든 페이지에 웹 구성 요소로 포함

> - 단일 페이지 애플리케이션(SPA)

> - 풀스택/서버측 렌더링(SSR)

> - Jamstack / 정적 사이트 생성(SSG)

> - 데스크톱, 모바일, WebGL, 심지어 터미널까지 타겟팅

### 단일 파일 구성 요소

> 대부분의 빌드 도구 지원 Vue 프로젝트에서 우리는 Single-File

> Component\*.vue ( 파일 이라고도 함 , 약어로 SFC ) 라는 HTML과 유사한 파일

> 형식을 사용하여 Vue 구성 요소를 작성

#### SFC 형식으로 작성된 이전 예

```javascript
<script setup>
import { ref } from "vue";
const count = ref(0);
</script>

<template>
  <button @click="count++">Count is: {{ count }}</button>
</template>

<style scoped>
button {
  font-weight: bold;
}
</style>
```

<hr/>

# Vue 환경셋팅

    ✅조건

    복합줄에 대한 지식
    Node.js 버전 16.0 이상 설치
    Visual Studio Code + Volar 확장

#### Extention 설치

- Vue 3 Snippets

- HTML CSS Support

- Vetur ❌ vue3이상 부터는 volar를 사용함

- ### Vue Language Features (Volar)

- 오류

<img width="426" alt="image" src="https://github.com/sin-hyunjin/Vue.js/assets/116487398/e85f440e-ecb8-4f58-b9af-114aa69679aa">

https://github.com/volarjs/services/tree/master/packages/vetur

### Installation

        npm install volar-service-vetur

volar.config.js

```
module.exports = {
	services: [
		require('volar-service-vetur').create(),
	],
};
```

이렇게 설정을 해주면 아래의 오류를 해결할 수 있다.

<img width="571" alt="image" src="https://github.com/volarjs/services/assets/116487398/8573bc40-b72e-47da-862d-0cada89a3609">

#### Vue 개발환경 셋팅 도움

    npm install -g @vue/cli

#### create-vue 설치하고 실행

    > npm create vue@latest

> 설치를 하면 몇가지 기능이 포함되어있음

 <img width="560" alt="image" src="https://github.com/sin-hyunjin/Vue.js/assets/116487398/64c99b4f-0772-4179-924a-3c3f967c479b">

#### 개발 서버 실행

    > cd <your-project-name>
    > npm install
    > npm run dev

#### When you are ready to ship your app to production, run the following:

    > npm run build
