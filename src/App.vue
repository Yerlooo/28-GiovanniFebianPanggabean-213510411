<template>
  <main>
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
    <header>
      <h1>Gioks Mart</h1>
    </header>

    <div class="new-task-form">
      <TaskForm/>
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">Semua</button>
      <button @click="filter = 'favs'">Kesukaan</button>
    </nav>
    
    <div class="task-list" v-if="filter === 'all'">
      <p>Kamu mempunyai {{ taskStore.tasks.length }} Belanjaan </p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>Kamu mempunyai {{ taskStore.favs.length }} belanja kesukaan</p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from 'vue';
import TaskDetails from './components/TaskDetails.vue';
import TaskForm from './components/TaskForm.vue';
import { useTaskStore } from './stores/TaskStore';

export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();
    const filter = ref('all');

    return { taskStore, filter };
  },
  computed: {
      filterClass() {
        return (value) => {
          return {
            active: this.filter === value,
          };
        };
      },
    },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
  margin-right: 10px;
}

nav a.router-link-exact-active {
  color: #42b983;
}

header {
  background-color: #f8f8f8;
  padding: 20px;
  margin-bottom: 30px;
}

h1 {
  font-size: 32px;
  margin: 0;
}

.filter {
  padding: 10px;
  background-color: #f8f8f8;
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
}

.filter button {
  padding: 8px 16px;
  margin-right: 10px;
  background-color: #42b983;
  color: #fff;
  border: none;
  cursor: pointer;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.filter button:hover {
  background-color: #3a9b72; /* Warna lebih gelap saat di hover */
}

.task-list {
  margin-top: 20px;
}

.task-list p {
  font-weight: bold;
  font-size: 18px;
  margin-bottom: 10px;
}

.task-list div {
  border: 1px solid #ddd;
  padding: 10px;
  margin-bottom: 10px;
  background-color: #f8f8f8;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.task-list div:hover {
  background-color: #e0e0e0;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3); /* Tambahkan efek bayangan saat di hover */
}

/* Tambahkan kelas CSS 'active' yang telah dihasilkan secara dinamis */
.filter button.active {
  background-color: #3a9b72;
}

.task-list p.empty {
  color: #888; /* Warna teks abu-abu untuk teks 'empty' */
  text-align: center;
}

.new-task-form {
  margin-bottom: 20px;
}

/* Gaya untuk responsif */
@media (max-width: 600px) {
  nav {
    padding: 15px;
  }

  header {
    padding: 15px;
  }

  h1 {
    font-size: 24px;
  }

  .filter {
    padding: 8px;
    margin-bottom: 10px;
  }

  .filter button {
    padding: 6px 12px;
    margin-right: 8px;
    font-size: 14px;
  }

  .task-list p {
    font-size: 16px;
    margin-bottom: 8px;
  }

  .task-list div {
    padding: 8px;
    margin-bottom: 8px;
  }
}
</style>