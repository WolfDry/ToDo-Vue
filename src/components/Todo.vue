<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: {}
    }
  },
  methods: {
    addTodo: function (form) {
      form.preventDefault()
      let date = new Date()
      date = date.toLocaleString('fr-FR')
      this.newTodo = {
        title: this.newTodo.title,
        createdAt: date,
        done: false
      }
      this.todos.push(this.newTodo)
      this.newTodo = {}
    },
    changeTodo: function (todo) {
      if (todo.done)
        todo.done = false
      else todo.done = true
    },
    deleteTodo: function (todo) {
      const listTodos = this.todos.filter(element => element != todo)
      this.todos = listTodos
    }
  }
}
</script>

<template>
  <div class="card">
    <form @submit="addTodo">
      <input v-model="newTodo.title" placeholder="Add Task">
      <button type="submit">Add</button>
    </form>
    <div class="list">
      <div class="todo" v-for="todo in todos">
        <p :class="{ done: todo.done }">{{ todo.title }}</p>
        <button @click="changeTodo(todo)">Done</button>
        <button @click="deleteTodo(todo)">Delete</button>
      </div>
    </div>

  </div>
</template>
