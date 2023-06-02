<template>
  <div id="app">
    <UserListContainer />
  </div>
</template>

<script>
import UserListContainer from './components/UserListContainer';

export default {
  name: 'App',
  components: {
    UserListContainer,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
