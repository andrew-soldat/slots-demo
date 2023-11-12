<template>
  <input v-model="filter" placeholder="search..." />
  <ul>
    <li v-for="item in filteredUsers" :key="item.id">
      <slot name="item" :item="item"></slot>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    fields: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      filter: '',
    }
  },
  computed: {
    filteredUsers() {
      return this.filter
        ? this.items.filter((u) =>
            this.fields.some((f) =>
              u[f].toLowerCase().includes(this.filter.toLowerCase())
            )
          )
        : this.items;
    }
  }
}
</script>