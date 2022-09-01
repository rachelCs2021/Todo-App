<template>
    <div 
         @click="$emit('update-todo', todo.id)"
         @dblclick="$emit('toggle-reminder', todo.id)" 
         :class="[ todo.reminder ? 'reminder' : '', 'todo']">

      <h3 :class="todo.priority">{{todo.title}} </h3>
        <i @click="$emit('delete-todo',todo.id)" class="fas fa-times"></i>
      <p>{{todo.description}}</p>
      <span class="date-of-todo">{{todo.date}}</span>
      <span class="repeat-of-todo">תדירות: {{todo.repeat}}</span>

    </div>
</template>

<script>

export default ({
  name: "TodoDetail",
  props: {
    todo: Object
  },
  date() {
    return {
     todo: this.todo
    }
  }
})
</script>

<style scoped>
  .todo{
    background-color: #fff;
    text-align: right;
    margin: 10px 15px;
    padding: 10px 15px;
    position: relative;
  }

  .todo.reminder {
    border-right: 5px solid rgb(205, 50, 200);
;
    text-decoration: line-through;
  }

  .fas {
    color: red;
    position: absolute;
    left: 13px;
    top: 20px;  
  }

  .date-of-todo{
    font-size: 13px;
    font-weight: 500;
  }

  .repeat-of-todo{
    font-size: 12px;
    margin-right: 10px;
  }

  .high{
     color: red;
  }
  .medium{
      color: black;
  }
  .low{
      color: rgb(205, 50, 200);
  }
</style>