<template>
  <div class="flex-row" role="columnheader">{{name}}</div>
</template>

<script>
export default {
  name: 'HeaderItem',
  props: {
    name: {
      type: String,
      default() {
        return [];
      },
    },
  },
};
</script>

<style>

</style>
