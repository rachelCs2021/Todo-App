<template>

<div class="container">
  <TodoHeader @btn-click="toggleAddTodo" :showAddTodo="showAddTodo" />
    <NewTodo v-show="showAddTodo"  @btn-click="toggleAddTodo" @add-todo="addTodo" />
  <TodoList @toggle-reminder="toggleReminder" @delete-todo="deleteTodo" :todos= "todos" @update-todo="updateTodo" />
</div>

</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoList from './components/TodoList.vue'
import NewTodo from "./components/NewTodo.vue"

export default {
  name: 'App',
  components: {
    TodoHeader,
    TodoList,
    NewTodo,
  },
  data() {
    return {
      todos: [],
      showAddTodo: false,
      priorityLevel: ''
    }
  },
  methods: {

    updateTodo(id) {
      console.log("update", id);
    },

    async addTodo(todo) {
      const res = await fetch('api/todos', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
         },
        body: JSON.stringify(todo)
     })
     const data = await res.json()
     this.todos = [...this.todos, data]
    },

    async deleteTodo(id) {
      if(confirm('האם אתה בטוח?')){

        const res = await fetch(`api/todos/${id}`, {
           method: 'DELETE',
        })
        res.status === 200 ? ( this.todos = this.todos.filter((todo) => todo.id !== id)) 
        : alert('Error deleting todo')
      }
    },

    async toggleReminder(id) {

     const todoToToggle = await this.fetchTodo(id)
     const updTodo = {...todoToToggle, reminder: !todoToToggle.reminder}

     const res = await fetch(`api/todos/${id}`, {
        method: 'PUT',
          headers: {
            'Content-type': 'application/json',
           },
         body: JSON.stringify(updTodo)
      })

      const data = await res.json()

      this.todos = this.todos.map((todo)=> todo.id === id ? {...todo, reminder: !data.reminder} : todo )
    },

    toggleAddTodo() {
      this.showAddTodo = !this.showAddTodo
    },
   async fetchTodos(){
      const res = await fetch('api/todos')

      const data = await res.json()
      return data
    },
   async fetchTodo(id){
      const res = await fetch(`api/todos/${id}`)

      const data = await res.json()
      return data
    }
  },

  async created() {
    this.todos = await this.fetchTodos()
  }
}

</script>

<style>
:root {
  --light: #eee;
}

#app {
  font-family: Avenir, Helvetica, Arial;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

*{
  margin: 0;
  padding: 0;
  direction: rtl;
}
body {
    background: var(--light);

}
</style>
