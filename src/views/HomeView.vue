<template>
  <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.12.1/css/all.min.css"
      integrity="sha256-mmgLkCYLUQbXn0B1SRqzHar6dCnv9oZFPEC1g1cwlkk="
      crossorigin="anonymous"
    />

  <h1>Gio Todo-List</h1>
  <div>
    <input class="form_input" v-model="newTodo" placeholder="Masukkan Kegiatan....">
    <i class="fas fa-plus-square" @click="addTodo"></i>
    <br><br>
    <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Tampilkan Semua' : 'Sembunyikan yang sudah selesai' }}</button>
    <ul>
      <li v-for="todo in visibleTodos" :key="todo.id">
        <span :class="{ 'completed': todo.completed }" @click="toggleComplete(todo)">{{ todo.text }}</span>
        <button v-if="!todo.completed" @click="completeTodo(todo.id)">Selesai</button>
        <button v-if="todo.completed" @click="unCompleteTodo(todo.id)">Belum Selesai</button>
        <button @click="removeTodo(todo.id)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      newTodo: '',
      nextId: 1,
      hideCompleted: false
    }
  },
  computed: {
    visibleTodos() {
      if (this.hideCompleted) {
        return this.todos.filter(todo => !todo.completed);
      } else {
        return this.todos;
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({
          id: this.nextId++,
          text: this.newTodo,
          completed: false
        });
        this.newTodo = '';
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    completeTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo) {
        todo.completed = true;
      }
    },
    unCompleteTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo) {
        todo.completed = false;
      }
    },
    toggleComplete(todo) {
      todo.completed = !todo.completed;
    }
  }
}
</script>

<style>
body {
  background-image: linear-gradient(120deg, #0c6f81 0%, #3a7d5e 100%);
  font-family: monospace;
  font-size: large;
  color: white;
}

ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

input {
  padding-top: 1rem;
  text-align: center;
  border-radius: 1%;
  border: 2px solid white;
}

.form_input {
    font-family: 'Roboto', sans-serif;
    color: #333;
    font-size: 1.2rem;
    margin: 0 auto;
    padding: 1.5rem 2rem;
    border-radius: 1rem;
    background-color: rgb(255, 255, 255);
    border: none;
    width: 90%;
    display: block;
    border-bottom: 0.3rem solid transparent;
    transition: all 0.3s;
  }

.completed {
  text-decoration: line-through;
}
button {
  margin-left: 10px;
}
</style>
