<template>
  <div class="flex-table row">
        <div class="flex-row" role="cell">{{user.name}}</div>
        <div class="flex-row" role="cell">{{user.phone}}</div>
        <UserList v-if="hasEmployees"/>
  </div>
</template>

<script>
import userList from '../data/user.list.json';

export default {
  name: 'UserItem',
  props: {
    user: {
      type: Object,
      default() {
        return [];
      },
    },
  },
  computed: {
    hasEmployees() {
      return this.user.employees.length > 0;
    },
  },
};
</script>

<style>

</style>
