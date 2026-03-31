<template>
  <div class="row">
    <div class="col">
      <ul class="list-group">
        <TodoListItem
          v-for="todoitem in todolist"
          :key="todoitem.id"
          :todoitem="todoitem"
          @delete-todo="emit('delete-todo', $event)"
          @checkbox-completed="emit('toggle-completed', $event)"
        />
        <!-- @checkbox-complited는 자식이 보낸 이벤트라 이름 맞춰야하지만, ('toggle-completed')는 app (부모)한테 보낼거라 이름 다르게 해도 됨 -->
        <!-- 이벤트 방출 시 전달되는 데이터는 $event로 수신 가능 , $event는 자식(TodolistItem) 한테 받은 데이터 값 -->
      </ul>
    </div>
  </div>
</template>
<script setup>
import TodoListItem from './TodoListItem.vue';

const props = defineProps({ todolist: { type: Array, required: true } });
const emit = defineEmits(['delete-todo', 'toggle-completed']);
</script>
