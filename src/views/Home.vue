<template>
  <div class="container">
    <div class="input">
      <input name="input" id="input" v-model="inputValue" @keyup.enter="handleInput"/>
      <button class="generate-button">Generate</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      inputValue: '',
      results: [],
    };
  },
  methods: {
    handleInput() {
      console.log(this.inputValue);
    },
  },
};
</script>

<style lang="scss" scoped>
  .container{
    display: flex;
    justify-content: center;
  }
</style>
