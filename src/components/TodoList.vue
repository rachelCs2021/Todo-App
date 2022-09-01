<template>
<div class="container-todos">
        <div v-for="todo in todos" :key="todo.id" todo="todo" >
       <TodoDetail 
         :key="todo"
         :todo="todo"
         @update-todo="$emit('update-todo', todo.id)"
         @toggle-reminder="$emit('toggle-reminder', todo.id)" 
         @delete-todo="$emit('delete-todo', todo.id)" 
        /> 
</div>
</div>

</template>

<script>
import TodoDetail from "./TodoDetail.vue"

export default {
  name: "TodoList",
  components: {
      TodoDetail
  },
  props: {
      todos: Array
  },
  emits: ['delete-todo', 'toggle-reminder', 'update-todo']
}
</script>

<style scoped>
   .container-todos{
       margin-bottom: 35px;
   }
</style>