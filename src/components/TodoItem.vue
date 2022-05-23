<template>
  <div class="todo-list" v-bind:class="{'is-complete': todo.completed}">
    <p>
      <input type="checkbox" v-on:change="markComplete" /> {{ todo.task }}
      <button @click="$emit('del-todo', todo.id)" class="del">x</button>
      <button @click="$emit('edit-todo', todo.id)" class="del">Edit</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  data() {
    return {
      tx: this.todo,
    };
  },
  methods: {
    markComplete() {
      this.tx.completed = !this.tx.completed;
    },
  },
};
</script>

<style scope>
.todo-list {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>
