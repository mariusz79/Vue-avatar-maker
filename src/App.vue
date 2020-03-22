<template>
<div>
    <div id="nav">
    <div  class="nav" :class="{'navShort':!navActive}">
      <div class="left">
      <router-link to="/">AvatarsMaker</router-link>
      </div>
      <div class="right" :class="{'hide':!navActive}">
      <router-link to="/about" class="aboutLink">About</router-link>
      <Login class="login"/>
      </div>
      <div class="hamburger" @click="navbarFunction()">
  <div class="bar1" :class="{'bar1nav':navActive}"></div>
  <div class="bar2" :class="{'bar2nav':navActive}"></div>
  <div class="bar3" :class="{'bar3nav':navActive}"></div>
</div>
    </div>
    </div>
    <router-view/>
    </div>

</template>

<script>
import Login from '@/components/Login.vue';

export default {
  name: 'App',
  components: {
    Login,
  },
  data() {
    return {
      navActive: false,
    };
  },
  methods: {
    navbarFunction() {
      this.navActive = !this.navActive;
    },
  },
};
</script>

<style lang="scss">
  #nav{
    position: absolute;
    top: 0;
    width: 100%;
  }
  .nav{
    padding: 8px;
    display: flex;
    flex-direction: column;
    align-items: center;
    background: #cae8e2;
    height: 170px;
    transition: height 0.3s ease-in-out;
  }
  .navShort{
    height: 30px;
    transition: height 0.3s ease-in-out;
    .left{
      margin-top: 10px;
      transition: 0.5s;
    }
  }
  a{
    text-decoration: none;
    color: #1fbc9c;
    font-size: 20px;
  }
  .left, .right, .login{
    margin-top: 20px;
    display: block;
  }
  .hide{
    visibility: hidden;
    opacity: 0;
    transition: visibility 0.3s opacity 0.3s;
  }
  .hamburger {
  display: inline-block;
  cursor: pointer;
  position: absolute;
  right: 10px;
}

.bar1, .bar2, .bar3 {
  width: 35px;
  height: 5px;
  background-color: #333;
  margin: 6px 0;
  transition: all 0.3s ease-in;
}

.bar1nav {
  -webkit-transform: rotate(-45deg) translate(-9px, 6px);
  transform: rotate(-45deg) translate(-9px, 6px);
}

.bar2nav{opacity: 0;}

.bar3nav{
  -webkit-transform: rotate(45deg) translate(-8px, -8px);
  transform: rotate(45deg) translate(-8px, -8px);
}
@media (min-width: 600px) {
  .hamburger {
    display: none;
  }
  .nav{
    flex-direction: row;
    justify-content: space-between;
  }
  .hide{
    visibility: visible;
    opacity: 1;
  }
  .left, .right, .login, .navShort .left{
    margin-top: 0;
  }
  .right{
    display: flex;
  }
  .aboutLink{
    margin-right: 18px;
  }
}
</style>
