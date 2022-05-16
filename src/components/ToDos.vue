<template>
  <div>
    <h1>Todos</h1>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <h3>{{ todo.title }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDos",
  props: ["todos"],
};
</script>

<style scoped></style>
