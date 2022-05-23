<template>
  <div>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="task" name="task" placeholder="Add Todo..." />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
// import uuid from "uuid";
export default {
  name: "AddTodo",
  data() {
    return {
      task: "",
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        // id: uuid,
        task: this.task,
        completed: false,
      };
      this.$emit("add-todo", newTodo);
      this.task = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}

input[type="text"] {
  flex: 10;
  padding: 5px;
}

input[type="submit"] {
  flex: 2;
}
</style>
