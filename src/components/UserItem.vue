<template>
  <div class="flex-table row">
        <div class="flex-row" role="cell">{{user.name}}</div>
        <div class="flex-row" role="cell">{{user.phone}}</div>
  </div>
</template>

<script>
import UserList from '../components/UserList';

export default {
  name: 'UserItem',
  components: { UserList },
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
