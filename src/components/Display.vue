<template>
<div>
  <div class="result" v-if="result">
      <img v-bind:src=result>
    </div>
</div>
</template>

<script>
export default {
  name: 'Display',
};
</script>

<style>

</style>
