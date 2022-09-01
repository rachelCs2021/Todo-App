<template>
    <header>
        <h1 class="title-todo">רשימת המטלות שלי</h1>
          <ButtonTodo 
              @btn-click="$emit('btn-click')" 
              :showAddTodo="showAddTodo"
              text="הוסף מטלה +"  />
    </header>
</template>

<script>
import ButtonTodo from "./ButtonTodo.vue"

export default ({
   name: "TodoHeader",
   components: {
           ButtonTodo,
   },
   props: {
       showAddTodo: Boolean
   },
   data() {
       return{
           name: '',
           time: ''
       }
   },
   method: {
       getTime() {
           let now = new Date()
           console.log(now);
       },
   }
 
 });
</script>

<style scoped>

   header{
       display: flex;
       justify-content: space-between;
       padding: 0 15px;
   }

   .title-todo {
       display: flex;
       color: black;
       text-shadow: 2px 2px 4px #ffffff;
   }
</style>