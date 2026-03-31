<template>
  <div id="app" class="container">
    <div class="card card-body bg-light">
      <div class="title">:: Todolist App</div>
    </div>
    <div class="card card-default panel-borderless">
      <div class="card-body">
        <InputTodo @addTodo="addTodo" />
        <TodoList
          :todolist="checkedTodo"
          @delete-todo="deleteTodo"
          @toggle-completed="toggleCompleted"
        />

        <!-- 자식한테 todolist라는 이름으로 checkedTodo 데이터를 전송한다 라는 의미   -->
      </div>
    </div>
  </div>
</template>

<script setup>
import TodoList from './components/TodoList.vue';
import InputTodo from './components/InputTodo.vue';
import { reactive, computed } from 'vue';
const ts = new Date().getTime();

const todoList = reactive([
  { id: ts, todo: '자전거 타기', completed: false },
  { id: ts + 1, todo: '딸과 공원 산책', completed: true },
  { id: ts + 2, todo: '일요일 애견 카페', completed: false },
  { id: ts + 3, todo: 'Vue 원고 집필', completed: false },
]);

// 할일 삭제
const deleteTodo = (id) => {
  if (confirm('정말로 삭제하시겠습니까?')) {
    let index = todoList.findIndex((ele) => id === ele.id);
    todoList.splice(index, 1);
  }
};
// 체크 박스 선택
const toggleCompleted = (id) => {
  let index = todoList.findIndex((item) => id == item.id);
  todoList[index].completed = !todoList[index].completed;
};

const addTodo = (todo) => {
  todoList.push({
    id: Date.now(),
    todo: todo,
    completed: false,
  });
};
const checkedTodo = computed(() => {
  const notDone = todoList.filter((item) => item.completed === false);
  const done = todoList.filter((item) => item.completed === true);
  return [...notDone, ...done];
});

// computed안에서 정의한 notDone,done 은 computed안에서만 쓸 수 있음
// script setup안의 return과 computed 안에서의 return은 다름 , 여기서 return 생략하면 todolist 없어짐
// ... 전개연산자 : 괄호안의 요소들을 하나씩 전개해라는 의미
</script>
