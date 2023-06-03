<template>
  <div class="flex-table header" role="rowgroup">
    <HeaderItem
      v-for="(header, index) in headers" :label="header.label" :name="header.name" :key="index"/>
  </div>
</template>

<script>
import HeaderItem from './HeaderItem';

export default {
  name: 'Header',
  components: { HeaderItem },
  props: {
    headers: {
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
