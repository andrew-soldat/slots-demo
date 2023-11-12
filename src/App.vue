<template>
  <ListItems :items="users" :fields="['name', 'username']">
    <template #item="slotProps">
      <Users :item="slotProps.item" />
    </template>
  </ListItems>
  <ListItems :items="todos" :fields="['title']">
    <template #item="slotProps">
      <Todos :item="slotProps.item" />
    </template>
  </ListItems>
</template>

<script>
import ListItems from "./components/ListItems.vue";
import Users from "./components/Users.vue";
import Todos from "./components/Todos";

import { loadUsers, loadTodos } from "./api";
export default {
  name: 'App',
  components: {
    ListItems,
    Users,
    Todos,
  },
  data() {
    return {
      users: [],
      todos: [],
    }
  },
  mounted() {
    loadUsers().then((users) => {
      this.users = users;
    });
    loadTodos().then((todos) => {
      this.todos = todos;
    });
  },
}
</script>
e
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
