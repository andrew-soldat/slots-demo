<template>
  <button @click="isPopupOpen = true">Popup</button>
  <Popup @close="isPopupOpen = false" @ok="popupConfirmed" :isOpen="isPopupOpen">
    Do you really want to cancel?
  </Popup>
  <hr>
  <ListItems :items="users" :fields="['name', 'username']">
    <template #item="slotProps">
      <Users :item="slotProps.item" />
    </template>
  </ListItems>
  <hr>
  <ListItems :items="todos" :fields="['title']">
    <template #item="slotProps">
      <Todos :item="slotProps.item" />
    </template>
  </ListItems>
</template>

<script>
import { loadUsers, loadTodos } from "./api";

import ListItems from "./components/ListItems.vue";
import Users from "./components/Users.vue";
import Todos from "./components/Todos";
import Popup from "@/components/Popup";

export default {
  name: 'App',
  components: {
    Popup,
    ListItems,
    Users,
    Todos,
  },
  data() {
    return {
      users: [],
      todos: [],
      isPopupOpen: false,
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
  methods: {
    popupConfirmed() {
      alert('Confiremed');
      this.isPopupOpen = false;
    }
  },
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
