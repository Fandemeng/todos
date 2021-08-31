<template>
  <div class="todo-item" :class="{'is-complete':todo.completed}">
    <p>
      <input type="checkbox" @change="markComplete" />
      {{ todo.title }}
      <button class="del" @click="$emit('deleteItem',todo.id)">x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["todo"],
  methods: {
      markComplete(){
         this.todo.completed = !this.todo.completed;
      }
  }
};
</script>

<style scoped >
.todo-item {
  background: #a3a6a2;
  padding: 10px;
  border-bottom: 1px #02595a dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #8a6e63;
  color: #dae0e3;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>

