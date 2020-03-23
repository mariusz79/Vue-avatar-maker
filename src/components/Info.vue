<template>
  <div class="info">
    <p>Generate avatars with initials from names.</p>
  </div>
</template>

<script>
export default {
  name: 'Info',
};
</script>

<style lang="scss" scoped>
  .info{
    text-align: center;
    display: flex;
    flex-direction: column;
    font-size: 29px;
    color:#1fbc9c;
    text-shadow: -4px -4px 10px rgba(255, 254, 255, 0.6), 0.7px 1px 1px
     rgba(35, 64, 94, 0.075), 3.5px 5px 3px
     rgba(35, 64, 94, 0.06), 6.3px 9px 5px rgba(35, 64, 94, 0.055), 9.1px 13px 7px
     rgba(35, 64, 94, 0.05), 11.9px 17px 9px rgba(35, 64, 94, 0.05);
  }
</style>
