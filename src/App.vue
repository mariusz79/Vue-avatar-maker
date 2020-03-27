<template>
<div>
    <div id="nav">
    <div  class="nav">
      <div class="left">
      <router-link to="/">AvatarsMaker</router-link>
      </div>
      <div class="right">
      <router-link to="/about" class="aboutLink">About</router-link>
      <Login class="login"/>
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
    };
  },
  methods: {
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
    justify-content: space-around;
    background: #efeff5;
    box-shadow: 0 2px 2px -2px rgba(0,0,0,.2);
  }
  a{
    text-decoration: none;
    color: #1fbc9c;
    font-size: 20px;
    &:hover{
      border-bottom: 1px solid green;
    }
  }
  .signin{
    margin-left: 25px;
  }
@media (max-width: 600px) {
   .signin{
    margin-left: 10px;
  }
  .nav{
    justify-content: space-between;
  }
}
@media (max-width: 400px) {
   a{
     font-size: 18px;
   }
}
</style>
