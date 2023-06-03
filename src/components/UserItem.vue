<template>
  <div :id="user.id" class="flex-table row">
        <div class="flex-row" role="cell">{{user.name}}</div>
        <div class="flex-row" role="cell">{{user.phone}}</div>
        <UserList :id="user.id" v-if="hasEmployees" :users="users"/>
  </div>
</template>

<script>
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
    users() {
      const rootUserList = this.$root.$children[0].$children[0];
      const allUsers = rootUserList.users;
      return allUsers.filter(user => user.parent === this.user.id);
    },
    hasEmployees() {
      return this.users.length > 0;
    },
  },
};
</script>

<style>

</style>
