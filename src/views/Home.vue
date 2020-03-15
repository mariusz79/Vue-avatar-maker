<template>
  <div class="container">
    <div class="input">
      <input name="input" id="input" v-model="inputValue" @keyup.enter="handleInput"/>
      <button class="generate-button">Generate</button>
    </div>
     <div class="result" v-if="result">
      <img v-bind:src=result>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      inputValue: '',
      result: [],
    };
  },
  methods: {
    handleInput() {
      axios.get(`https://eu.ui-avatars.com/api/?name=${this.inputValue}`)
        .then((response) => {
          this.result = (response.config.url);
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
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
