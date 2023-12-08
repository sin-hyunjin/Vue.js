<script setup>
// Vue의 Composition API에서 사용할 수 있는 스크립트 설정 방식을 사용

// ref 함수를 사용하여 반응형 변수를 생성
import { ref, onMounted, computed, watch } from "vue";
const todos = ref([]); // 할 일 목록을 저장하는 배열
const name = ref(""); // 사용자의 이름을 저장하는 변수

// 입력 필드의 내용과 카테고리를 저장하는 변수
const input_content = ref("");
const input_category = ref(null);

// 생성일을 기준으로 정렬된 할 일 목록을 반환하는 계산된 속성
const todos_asc = computed(() =>
  todos.value.sort((a, b) => {
    return a.createdAt - b.createdAt;
  })
);

// name 변수의 변경을 감시하고 로컬 스토리지에 저장
watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

// todos 배열의 변경을 감시하고 로컬 스토리지에 저장 (깊은 감시 활성화)
watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  {
    deep: true,
  }
);

// 할 일을 추가하는 함수
const addTodo = () => {
  // 입력 필드가 비어있거나 카테고리가 선택되지 않았을 경우 함수 종료
  // trim() 공백제거
  if (input_content.value.trim() === "" || input_category.value === null) {
    return;
  }

  // 새로운 할 일을 todos 배열에 추가
  todos.value.push({
    content: input_content.value,
    category: input_category.value,
    done: false,
    editable: false,
    createdAt: new Date().getTime(),
  });
};

// 특정 할 일을 삭제하는 함수
const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo);
};

// 컴포넌트가 마운트되면 로컬 스토리지에서 사용자 이름과 할 일 목록을 가져와서 설정
onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todos")) || [];
});
</script>

<template>
  <!-- 메인 애플리케이션 컨테이너 -->
  <main class="app">
    <!-- 인사 섹션 -->
    <section class="greeting">
      <!-- 인사 제목과 사용자 이름을 입력하는 입력란 -->
      <h2 class="title">
        안녕하세요,
        <input
          type="text"
          id="name"
          placeholder="이름을 입력하세요"
          v-model="name"
        />
      </h2>
    </section>

    <!-- 할 일 추가 섹션 -->
    <section class="create-todo">
      <!-- 새로운 할 일을 만들기 위한 제목 -->
      <h3>할 일 추가</h3>

      <!-- 새로운 할 일을 추가하는 폼 -->
      <form id="new-todo-form" @submit.prevent="addTodo">
        <!-- 할 일 내용을 입력하는 입력란 -->
        <h4>할 일 목록에 무엇이 있나요?</h4>
        <input
          type="text"
          name="content"
          id="content"
          placeholder="예: 동영상 만들기"
          v-model="input_content"
        />

        <!-- 할 일 카테고리 선택 -->
        <h4>카테고리 선택</h4>
        <div class="options">
          <!-- 비즈니스 카테고리 선택 라디오 버튼 -->
          <label>
            <input
              type="radio"
              name="category"
              id="category1"
              value="business"
              v-model="input_category"
            />
            <span class="bubble business"></span>
            <div>비즈니스</div>
          </label>

          <!-- 개인 카테고리 선택 라디오 버튼 -->
          <label>
            <input
              type="radio"
              name="category"
              id="category2"
              value="personal"
              v-model="input_category"
            />
            <span class="bubble personal"></span>
            <div>개인</div>
          </label>
        </div>

        <!-- 할 일 추가 버튼 -->
        <input type="submit" value="할 일 추가" />
      </form>
    </section>

    <!-- 할 일 목록 섹션 -->
    <section class="todo-list">
      <!-- 할 일 목록 제목 -->
      <h3>할 일 목록</h3>
      <!-- 할 일 목록을 표시하는 영역 -->
      <div class="list" id="todo-list">
        <!-- 할 일 항목 반복 표시 -->
        <div
          v-for="todo in todos_asc"
          :class="`todo-item ${todo.done && 'done'}`"
        >
          <!-- 체크박스와 할 일 카테고리를 표시하는 영역 -->
          <label>
            <input type="checkbox" v-model="todo.done" />
            <span
              :class="`bubble ${
                todo.category == 'business' ? 'business' : 'personal'
              }`"
            ></span>
          </label>

          <!-- 할 일 내용을 편집하는 입력란 -->
          <div class="todo-content">
            <input type="text" v-model="todo.content" />
          </div>

          <!-- 할 일 삭제 버튼 -->
          <div class="actions">
            <button class="delete" @click="removeTodo(todo)">삭제</button>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
