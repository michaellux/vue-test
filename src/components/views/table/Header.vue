<template>
  <div class="flex-table header" role="rowgroup">
    <HeaderItem v-for="(name, index) in names" :name="name" :key="index"/>
  </div>
</template>

<script>
import HeaderItem from './HeaderItem';

export default {
  name: 'Header',
  components: { HeaderItem },
  props: {
    names: {
      type: Array,
      default() {
        return [];
      },
    },
  },
};
</script>

<style>

</style>
