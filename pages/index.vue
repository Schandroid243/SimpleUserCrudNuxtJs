<template>

</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  created() {
    this.$router.push({name: 'users-add'});
  }
})
</script>
<style scoped>
  .myColor {
    background-color: red
  }
  .rowTitle {
    margin-top: 105px;
  }
</style>
