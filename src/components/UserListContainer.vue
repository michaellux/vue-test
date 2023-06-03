<template>
    <div class="container">
      <a class="button" href="#popup">Добавить</a>
      <UserList :isRoot="isRoot" :users="users"/>
      <AddUserItemPopUp :users="users"/>
    </div>
</template>

<script>
import UserList from './UserList';
import AddUserItemPopUp from './AddUserItemPopup';

import userList from '../data/user.list.json';

export default {
  components: {
    UserList, AddUserItemPopUp,
  },
  data() {
    return {
      isRoot: true,
      users: [],
    };
  },
  mounted() {
    if (localStorage.getItem('users') != null) {
      try {
        this.users = JSON.parse(localStorage.getItem('users'));
      } catch (e) {
        this.users = userList;
      }
    } else {
      this.users = userList;
    }
  },
};
</script>

<style>
.container {
  margin: 2em;
}

.button {
    background-color: #4CAF50;
    border: none;
    color: white;
    padding: 1rem 2rem;
    border-radius: 2rem;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin-bottom: 2rem;
}
</style>
