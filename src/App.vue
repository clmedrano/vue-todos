<template>
  <!-- <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App xx"/>
  </div> -->
  <div>
    <div id="header">
      <Search v-on:query-change="buscador" />
    </div>
    <div id="main-container">
      <h2>Todos</h2>
      <TodoAdd v-on:add-todo="addTodo" />
      <TodosDatos v-bind:todosList="copyTodos" v-on:delete-todo="deleteTodo" />
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Search from "./components/Search.vue";
import TodosDatos from "./components/Todos.vue";
import TodoAdd from "./components/TodoAdd.vue";

let time;
export default {
  name: "App",
  components: {
    // HelloWorld
    TodosDatos,
    TodoAdd,
    Search,
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id != id);
      this.copyTodos = [...this.todos];
    },
    addTodo(todo) {
      this.todos.push(todo);
      this.copyTodos = [...this.todos];
    },
    buscador(query) {
      clearTimeout(time);
      time = setTimeout(() => {
        if (query.trim() === "") {
          this.copyTodos = [...this.todos];
        } else {
          const temp = this.todos.filter((todo) => {
            return todo.title.includes(query);
          });
          this.copyTodos = [...temp];
        }
      }, 400);
    },
  },
  data() {
    return {
      todos: [
        { id: 0, title: "Tarea Nro 1", completed: false },
        { id: 1, title: "Tarea Nro 2", completed: true },
        { id: 2, title: "Tarea Nro 3", completed: false },
      ],
      copyTodos: [],
    };
  },
  created() {
    this.copyTodos = [...this.todos];
  },
};
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

* {
  box-sizing: border-box;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1.5em;
  padding: 0;
  margin: 0;
}
#main-container {
  border: 1px solid #ccc;
  width: 600px;
  margin: 100px auto;
}
#header {
  background: black;
  padding: 10px;
}
h2 {
  padding: 0 10px;
}
</style>
