<template>
<div>
 <div class="display">
        </div>
</div>
</template>

<script>
export default {
  name: 'Display',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss">
 .showResult{
    display: flex;
    justify-content: center;
    margin-top: 15px;
  }
  .showResult{
    margin-top: 30px;
    display: flex;
    flex-direction: column;
    text-align: center;

    p{
      color: grey;
    }
  }
</style>
