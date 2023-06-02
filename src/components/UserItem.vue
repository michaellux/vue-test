<template>
  <div class="flex-table row">
        <div class="flex-row" role="cell">{{user.name}}</div>
        <div class="flex-row" role="cell">{{user.phone}}</div>
        <UserList :id="user.id" v-if="hasEmployees" :users="users"/>
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
      return userList.filter(user => user.parent === this.user.id).length > 0;
    },
    users() {
      return userList.filter(user => user.parent === this.user.id);
    },
  },
};
</script>

<style>

</style>
