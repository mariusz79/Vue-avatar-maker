<template>
  <div class="container">
    <Info />
    <div class="input">
      <input name="input" id="input" v-model="inputValue" @keyup.enter="handleInput()"/>
      <button class="generate-button" @click="handleInput()">Generate</button>
      <input type="checkbox" id="roundedValue" v-model="roundedValue" @click="handleInput();
       handleRounded();">
      <label for="roundedValue">Rounded</label>
      <input type="checkbox" id="uppercaseValue" v-model="uppercaseValue" @click="handleInput();
       handleUppercase();">
      <label for="uppercaseValue">Uppercase</label>
      <input type="checkbox" id="boldValue" v-model="boldValue" @click="handleInput();
       handleBold();">
      <label for="boldValue">Bold</label>
    </div>
     <div class="result" v-if="result">
      <img v-bind:src=result>
    </div>
  </div>
</template>

<script>
import Info from '@/components/Info.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Info,
  },
  data() {
    return {
      inputValue: '',
      roundedValue: false,
      uppercaseValue: false,
      boldValue: false,
      result: [],
    };
  },
  methods: {
    handleInput() {
      axios.get(`https://eu.ui-avatars.com/api/?name=${this.inputValue}&rounded=${this.roundedValue}&bold=${this.boldValue}&uppercase=${this.uppercaseValue}`)
        .then((response) => {
          this.result = (response.config.url);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    handleRounded() {
      this.roundedValue = !this.roundedValue;
      this.handleInput();
    },
    handleUppercase() {
      this.uppercaseValue = !this.uppercaseValue;
      this.handleInput();
    },
    handleBold() {
      this.boldValue = !this.boldValue;
      this.handleInput();
    },
  },
};
</script>

<style lang="scss" scoped>
  .container{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
</style>
