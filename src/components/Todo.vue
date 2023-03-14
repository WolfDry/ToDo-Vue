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
      <div class="todo" v-for="(todo, index) in todos">
        <p>{{ todo.title }}</p>
        <button>Done</button>
      </div>
    </div>
    <div class="complete">

    </div>

  </div>
</template>
