<template>
  <div class="container">
    <button class="button">Добавить</button>
    <UserList :isRoot="isRoot" :users="users"/>
  </div>
</template>

<script>
import UserList from './UserList';
import userList from '../data/user.list.json';

export default {
  components: {
    UserList,
  },
  data() {
    return {
      isRoot: true,
      users: userList,
    };
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
