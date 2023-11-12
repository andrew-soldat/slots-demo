<template>
  <users-list :users="users" />
</template>

<script>
import UsersList from "./components/UsersList.vue";

import { loadUsers } from "./api";
export default {
  name: 'App',
  components: {
    UsersList,
  },
  data() {
    return {
      users: [],
    }
  },
  mounted() {
    loadUsers().then((users) => {
      this.users = users;
    });
  }
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
