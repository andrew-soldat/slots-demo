<template>
  <input v-model="filter" placeholder="search..." />
  <ul>
    <li v-for="user in filteredUsers" :key="user.id">{{ user.name }} {{ user.username }}</li>
  </ul>
</template>

<script>
export default {
  props: {
    users: {
      type: Array,
      required: true,
    }
  },
  data() {
    return {
      filter: '',
    }
  },
  computed: {
    filteredUsers() {
      return this.filter
        ? this.users.filter((u) =>
            [u.name, u.username].some((v) =>
              v.toLowerCase().includes(this.filter.toLowerCase())
            )
          )
        : this.users;
    }
  }
}
</script>