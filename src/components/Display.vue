<template>
<div>
  <div class="showResult">
     <div class="result" v-if="result">
      <img v-bind:src=result>
    </div>
    <p>Right-click on avatar and select 'Save image as ...'</p>
  </div>
</div>
</template>

<script>
export default {
  name: 'Display',
  props: {
    result: {
      type: String,
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
