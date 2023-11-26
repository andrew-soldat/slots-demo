<template>
  <button @click="popupOpen">Popup</button>
  <Popup @close="isPopupOpen = false" @ok="popupConfirmed" :isOpen="isPopupOpen">
    Do you really want to cancel?
    <template #action="{ confirmed }">
      <span>Write</span>
      <input class="popup__input" v-model="confirmation" :placeholder="$options.CONFIRMATION_TEXT" />
      <button class="popup__btn" @click="confirmed" :disabled="!isConfirmationCorrect">OK</button>
    </template>
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
      confirmation: '',
    }
  },
  CONFIRMATION_TEXT: 'CONFIRM',
  mounted() {
    loadUsers().then((users) => {
      this.users = users;
    });
    loadTodos().then((todos) => {
      this.todos = todos;
    });
  },
  methods: {
    popupOpen() {
      this.isPopupOpen = true;
      this.confirmation = '';
    },
    popupConfirmed() {
      alert('Confiremed');
      this.isPopupOpen = false;
    },
  },
  computed: {
    isConfirmationCorrect() {
      return this.confirmation === this.$options.CONFIRMATION_TEXT;
    },
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
