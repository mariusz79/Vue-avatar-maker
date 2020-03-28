<template>
  <div class="container">
    <div class="insideContainer">
    <Info />
    <div class="inputs">
      <input type="text" name="input" id="input" placeholder="Type your name..."
      v-model="inputValue" @keyup.enter="handleInput()"/>
    </div>
    <div class="checkboxes">
      <input type="checkbox" id="roundedValue" v-model="roundedValue"
      :class="{'checkboxActive':roundedValue}" @click="handleRounded();">
      <label for="roundedValue" :class="{'grey':!roundedValue}">Rounded</label>
      <input type="checkbox" id="uppercaseValue" v-model="uppercaseValue"
      @click="handleUppercase();" :class="{'checkboxActive':uppercaseValue}">
      <label class="uppercaseValue" :class="{'grey':!uppercaseValue}"
      for="uppercaseValue">Uppercase</label>
      <input type="checkbox" id="boldValue" v-model="boldValue"
      @click="handleBold();" :class="{'checkboxActive':boldValue}">
      <label for="boldValue" :class="{'grey':!boldValue}">Bold</label>
    </div>
    <div class="custom">
      <div class="colors">
      <div class="backgroundColors">
      <div><swatches v-model="background"></swatches></div><p class="description">Background</p>
      </div>
      <div class="lettersColors">
      <div><swatches v-model="color"></swatches></div><p class="description">Color</p>
      </div>
      </div>
      <div class="slider">
       <div><circle-slider :min="16"
            :max="512"
            :step-size="1"
            id="sizeValue" v-model="sizeValue"></circle-slider></div>
            <p class="sizeValue">Size: {{ sizeValue }}</p>
        </div>
    </div>
    <div class="genButton">
      <button class="generateButton" @click="handleInput()">Generate</button>
    </div>
    <div class="showResult">
     <div class="result" v-if="result">
      <img v-bind:src=result>
    </div>
    <p>Right-click on avatar and select 'Save image as ...'</p>
    </div>
    <div v-if="$auth.isAuthenticated && result!=''" class="save">
    <button @click="post()">Save</button>
    </div>
    <div v-if="$auth.isAuthenticated" class="history">
      <button @click="get()">Load your avatars</button>
      <div class="items">
      <div v-for="key in userdata" :key="userdata[key]">
        <img v-bind:src=key.body class="item">
        </div>
      </div>
    </div>
  </div>
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
      background: '#1fbc9c',
      color: '#BDC3C8',
      result: [],
      user: '',
      body: '',
      userdata: [],
      item: {
        type: Object,
        required: true,
      },
    };
  },
  methods: {
    login() {
      this.$auth.loginWithRedirect();
    },
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
        body: this.result,
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
        .then((response) => {
          this.userdata = response.data;
          console.log(response.data);
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
    margin-top: 50px;
    display: flex;
    justify-content: center;
  }
  .inputs, .checkboxes, .genButton, .showResult{
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
  #input{
    min-width: 35vw;
  }
  .backgroundColors, .lettersColors{
    display: flex;
  }
  .custom{
    display: flex;
    justify-content: space-evenly;
    margin-top: 15px;
  }
  .colors{
    display: flex;
    flex-direction: column;
    margin-left: 6vw;
  }
  .description{
    margin-left: 5px;
  }
  input, button {
    letter-spacing: -0.2px;
    font-size: 16px;
  }
  input {
  margin-right: 16px/2;
  box-shadow:  inset 2px 2px 5px #BABECC, inset -5px -5px 10px #FFF;
  box-sizing: border-box;
  transition: all 0.2s ease-in-out;
  appearance: none;
  -webkit-appearance: none;
 }
 input[type="text"]:focus {
    box-shadow:  inset 1px 1px 2px #BABECC, inset -1px -1px 2px #FFF;
  }
 button {
  color:#11AE8E;
  box-shadow: -5px -5px 20px #FFF,  5px 5px 20px  #BABECC;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
  font-weight: 600;
  &:hover {
    box-shadow: -2px -2px 5px #FFF, 2px 2px 5px  #BABECC;
  }
  &:active {
    box-shadow: inset 1px 1px 2px  #BABECC, inset -1px -1px 2px #FFF;
  }
 }
 button, input {
  border: 0;
  outline: 0;
  font-size: 16px;
  border-radius: 16px*20;
  padding: 16px;
  background-color: #EBECF0;
  text-shadow: 1px 1px 0 #FFF;;
  }
  .checkboxActive {
    box-shadow:  inset 1px 1px 2px rgb(89, 172, 95), inset -1px -1px 2px rgb(6, 226, 68);
  }
  .card{
    display: flex;
    padding: 16px;
    box-shadow: -2px -2px 5px #FFF, 2px 2px 5px  #BABECC;
  }
  .sizeValue{
    position: relative;
    top: 22px;
    right: 76px;
    color: darkcyan;
  }
  .checkboxes label{
    margin-top: 10px;
  }
  .slider{
    display: flex;
  }
  #uppercaseValue{
    margin-left: 3vw;
  }
  .uppercaseValue{
    margin-right: 3vw;
  }
  .insideContainer{
    max-width: 800px;
  }
  .generateButton{
    width: 200px;
  }
  .grey{
    color: grey;
  }
  .history{
    margin-top: 15px;
    text-align: center;
  }
  .save{
    text-align: center;
  }
  .items{
    display: flex;
    flex-wrap: wrap;
  }
  .item{
    margin: 10px;
  }
  @media (max-width: 600px) {
    #input{
      min-width: 71vw;
    }
    .colors{
      margin-left: 18vw;
    }
  }
</style>
