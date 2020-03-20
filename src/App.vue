<template>
  <div id="app">
    <div>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
      <Login />
    </div>
    <router-view/>
    </div>
  </div>
</template>

<script>
import Login from '@/components/Login.vue';

export default {
  name: 'App',
  components: {
    Login,
  },
};
</script>

<style lang="scss">

</style>
