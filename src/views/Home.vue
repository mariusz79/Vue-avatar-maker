<template>
  <div class="container">
    <Info />
    <div class="input">
      <input name="input" id="input" v-model="inputValue" @keyup.enter="handleInput()"/>
      <button class="generate-button" @click="handleInput()">Try</button>
      <input type="checkbox" id="roundedValue" v-model="roundedValue" @click="handleInput();
       handleRounded();">
      <label for="roundedValue">Rounded</label>
      <input type="checkbox" id="uppercaseValue" v-model="uppercaseValue" @click="handleInput();
       handleUppercase();">
      <label for="uppercaseValue">Uppercase</label>
      <input type="checkbox" id="boldValue" v-model="boldValue" @click="handleInput();
       handleBold();">
      <label for="boldValue">Bold</label>
       <circle-slider :min="16"
            :max="512"
            :step-size="1"
            id="sizeValue" v-model="sizeValue"></circle-slider>
      <div>{{ sizeValue }}</div>
      <button class="generate-button" @click="handleInput()">Generate</button>
    </div>
    <div>
    <swatches v-model="background"></swatches>
    <swatches v-model="color"></swatches>
  </div>
     <div class="result" v-if="result">
      <img v-bind:src=result>
    </div>
    <button @click="post()">Post</button>
    <button @click="get()">Get</button>
    <button @click="pri()">P</button>
    <div v-if="blo">{{blo}}</div>
  </div>
</template>

<script>
import Info from '@/components/Info.vue';
import axios from 'axios';
import VueCircleSlider from 'vue-circle-slider';
import Vue from 'vue';
import Swatches from 'vue-swatches';
import 'vue-swatches/dist/vue-swatches.min.css';

Vue.use(VueCircleSlider);
Vue.use(Swatches);

export default {
  name: 'App',
  components: {
    Info, Swatches,
  },
  data() {
    return {
      inputValue: '',
      roundedValue: false,
      uppercaseValue: false,
      boldValue: false,
      sizeValue: 64,
      background: '#1CA085',
      color: '#F493A7',
      result: [],
      user: '',
      body: '2',
      blo: [],
    };
  },
  methods: {
    handleInput() {
      const backgroundColor = this.background.slice(1);
      const fontColor = this.color.slice(1);
      axios.get(`https://eu.ui-avatars.com/api/?name=${this.inputValue}
      &rounded=${this.roundedValue}&bold=${this.boldValue}&uppercase=${this.uppercaseValue}
      &size=${this.sizeValue}&background=${backgroundColor}&color=${fontColor}`)
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
    handleSize() {
      this.handleInput();
    },
    pri() {
      console.log(this.$auth.user.nickname);
    },
    post() {
      console.log(this.$auth.user.nickname);
      this.user = this.$auth.user.nickname;
      axios.post(`https://vue-avatar-maker.firebaseio.com/${this.user}.json`, {
        body: this.body,
      }).then((data) => {
        console.log(data);
      })
        .catch((error) => {
          console.log(error);
        });
    },
    get() {
      this.user = this.$auth.user.nickname;
      axios.get(`https://vue-avatar-maker.firebaseio.com/${this.user}.json`)
        .then((data) => {
          this.blo.push(data);
          console.log(data);
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
    align-items: center;
    flex-direction: column;
  }
</style>
