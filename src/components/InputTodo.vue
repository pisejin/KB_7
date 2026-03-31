<template>
  <div class="row mb-3">
    <div class="col">
      <div class="input-group">
        <input
          type="text"
          class="form-control"
          placeholder="할일을 여기에 입력!"
          v-model="todo"
          @keyup.enter="addTodoHandler"
        />
        <button class="btn btn-primary" type="button" @click="addTodoHandler">
          추가
        </button>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from 'vue';

const todo = ref('');

const addTodoHandler = () => {
  // 할 일이 3글자 이상인 경우에만
  if (todo.value.length >= 3) {
    emit('addTodo', todo.value);
    todo.value = '';
  } else {
    alert('할 일은 3글자 이상 입력해주세요.');
  }
};

const emit = defineEmits(['addTodo']);
//이벤트 방출 검사
// -> 부모 컴포넌트로 전달되는 이벤트가 addTodo가 맞는지 검사
</script>
