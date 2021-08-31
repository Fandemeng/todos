<template>
  <div id="app">

    <AddTodo @handleAdd="handleAdd" />
    <Todos :todos="todos" @handleDelete="handleDelete" />
  </div>
</template>
<script>
import Todos from "../components/Todos.vue";

import AddTodo from "../components/AddTodo";
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      msg: "hello",
      todos: [
        {
          id: 1,
          title: "待办事项1",
          completed: false,
        },
        {
          id: 2,
          title: "待办事项2",
          completed: false,
        },
        {
          id: 3,
          title: "待办事项3",
          completed: false,
        },
      ],
    };
  },
  components: {
    Todos,  
    AddTodo,
  },
  methods: {
    handleDelete(id) {
      axios
        .delete(`http://jsonplaceholder.typicode.com/todos/${id}`)
        .then(
          (res) => (this.todos = this.todos.filter((todo) => todo.id !== id))
        )
        .catch((err) => console.log(err));
    },
    handleAdd(newTodo) {
      // this.todo.unshift(newTodo);
      this.todos = [...this.todos, newTodo];

      const { title, completed } = newTodo;
      // const title = newTodo.title;
      // const completed = newTodo.completed;
      axios
        .post("http://jsonplaceholder.typicode.com/todos", {
          title,
          completed,
        })
        .then((res) => (this.todos = [res.data, ...this.todos]))
        .catch((err) => console.log(err));
    },
  },
  created() {
    //数据请求
    axios
      .get("http://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => {
        this.todos = res.data;
      })
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
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #000917;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #000917;
}
</style>
