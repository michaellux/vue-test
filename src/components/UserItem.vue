<template>
  <div class="flex-table row">
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
    hasEmployees() {
      const users = this.$parent.$props.users;
      return users.filter(user => user.parent === this.user.id).length > 0;
    },
    users() {
      const users = this.$parent.$props.users;
      return users.filter(user => user.parent === this.user.id);
    },
  },
};
</script>

<style>

</style>
