<template>
  <div class="todo-list">
    <!-- 根据复选框的状态，修改isComplete状态， -->
    <ToDoItem
      v-for="(todo,index) in todos"
      :key="index"
      :todo="todo"
      @change-state="todo.isComplete = $event.target.checked"
      v-on="$listeners"
    ></ToDoItem>
  </div>
</template>

<script>
import ToDoItem from './ToDoItem.vue'
export default {
  name: 'ToDoList',
  components: {
    ToDoItem
  },
  props: ['todos']// 接收父组件的todos
}
</script>

<style lang="less">
</style>
