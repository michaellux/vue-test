<template>
  <div :id="user.id" class="flex-table row" @click.stop="switchShowEmployee">
        <div class="flex-row" role="cell">
          <span>{{
            hasEmployees ?
            (showEmployees === true ? '-' : '+') : ''
          }}</span>
          {{user.name}}
        </div>
        <div class="flex-row" role="cell">{{user.phone}}</div>
        <UserList :id="user.id" v-if="hasEmployees" v-show="showEmployees" :users="users"/>
  </div>
</template>

<script>
export default {
  name: 'UserItem',
  data() {
    return {
      showEmployees: true,
    };
  },
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
  methods: {
    switchShowEmployee() {
      debugger;
      if (this.hasEmployees) {
        this.showEmployees = !this.showEmployees;
      }
    },
  },
};
</script>

<style>

</style>
