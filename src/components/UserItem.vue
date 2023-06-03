<template>
  <div :id="user.id"
    class="flex-table row"
     @click.stop="switchShowEmployee">
    <div class="wrapper" :class="hasEmployees ? classRowHoverEffect : ''">
    <div class="flex-row">
          <div class="cell" role="cell">
              <span>{{
                hasEmployees ?
                (showEmployees === true ? '-' : '+') : ''
              }}</span>
              {{user.name}}
          </div>
    </div>

    <div class="flex-row">
          <div class="cell" role="cell">{{user.phone}}</div>
    </div>
    </div>
    <UserList :id="user.id" v-if="hasEmployees" v-show="showEmployees" :users="users"/>
  </div>
</template>

<script>
export default {
  name: 'UserItem',
  data() {
    return {
      showEmployees: true,
      classRowHoverEffect: {
        'row-hovereffect': true,
      },
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
      if (this.hasEmployees) {
        this.showEmployees = !this.showEmployees;
      }
    },
  },
};
</script>

<style>
.wrapper {
  width: 100%;
  display: flex;
  flex-direction: row;
}
.cell {
  width: 100%;
}

.row-hovereffect:hover {
  cursor: pointer;
  font-weight: bolder;
}
</style>
