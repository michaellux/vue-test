<template>
  <div @click="sortUsers(label)" class="flex-row" role="columnheader">{{name}}</div>
</template>

<script>
export default {
  name: 'HeaderItem',
  props: {
    label: {
      type: String,
      default() {
        return '';
      },
    },
    name: {
      type: String,
      default() {
        return '';
      },
    },
  },
  methods: {
    sortUsers(label) {
      const rootUserList = this.$root.$children[0].$children[0];
      const allUsers = rootUserList.users;
      if (label === 'name') {
        this.sortByName(allUsers, label);
      } else if (label === 'phone') {
        this.sortByPhone(allUsers, label);
      }
    },
    // https://medium.com/swlh/filtering-sorting-and-searching-in-arrays-with-vue-js-f60951c040fc
    sortByName(allUsers, label) {
      allUsers.sort((a, b) => {
        const fa = a[label].toLowerCase();
        const fb = b[label].toLowerCase();
        if (fa < fb) {
          return -1;
        }
        if (fa > fb) {
          return 1;
        }
        return 0;
      });
    },
    sortByPhone(allUsers, label) {
      allUsers.sort((a, b) => {
        const fa = a[label].replace(/\D/g, '');
        const fb = b[label].replace(/\D/g, '');
        if (fa < fb) {
          return -1;
        }
        if (fa > fb) {
          return 1;
        }
        return 0;
      });
    },
  },
};
</script>

<style>

</style>
