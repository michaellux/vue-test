<template>
  <div id="app">
    <UserList :isRoot="isRoot" :users="users"/>
  </div>
</template>

<script>
import UserList from './components/UserList';
import userList from './data/user.list.json';

export default {
  name: 'App',
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
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
