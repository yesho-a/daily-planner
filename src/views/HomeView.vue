<template>
  <AddTodo v-on:add-todo="addTodo" />
  <ToDos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
</template>

<script>
//import HelloWorld from "./components/HelloWorld.vue";
import ToDos from "../components/ToDos.vue";
import AddTodo from "../components/AddTodo.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    ToDos,
    AddTodo,
  },
  data() {
    return {
      todos: [
        // {
        //   id: 1,
        //   title: "Todo One",
        //   completed: false,
        // },
        // {
        //   id: 2,
        //   title: "Todo Two",
        //   completed: true,
        // },
        // {
        //   id: 3,
        //   title: "Todo Three",
        //   completed: false,
        // },
      ],
    };
  },
  methods: {
    // deleteTodo(id) {
    //   this.todos = this.todos.filter((todo) => todo.id !== id);
    // },
    deleteTodo(id) {
      axios
        .delete(`http://127.0.0.1:8000/api/delete/{id}/${id}`)
        .then(() => (this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((err) => console.log(err));
    },
    // addTodo(newTodo) {
    //   this.todos = [...this.todos, newTodo];
    // },

    addTodo(newTodo) {
      const {task, completed} = newTodo;

      axios
        .post("http://127.0.0.1:8000/api/tasks/create", {
          task,
          completed,
        })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));
    },
  },

  created() {
    axios
      .get("http://127.0.0.1:8000/api/tasks")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 2.4d;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
