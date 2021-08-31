<template>
  <div>
    <div :key="index" v-for="(todo, index) in todos">
      <!-- <TodoItem :todo="todo" @deleteItem="deleteItem" /> -->
      <TodoItem :todo="todo" @deleteItem="$emit('handleDelete',todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  name: "Todos",
  //从app.vue传值  方法一
  //   props:["todo"]

  //从app.vue传值  方法二
  props: {
    todos: {
      type: Array,
    },
  },
  //声明所调用的组件
  components: {
    TodoItem,
  },
  methods:{
      deleteItem(id){


      }
  }
};
</script>

<style scoped>
</style>

