<template>
      <!-- Check that the SDK client is not currently loading before accessing is methods -->
      <div v-if="!$auth.loading" class="signin">
        <!-- show login when not authenticated -->
        <a v-if="!$auth.isAuthenticated" @click="login">
          Sign in</a>
        <!-- show logout when authenticated -->
        <a v-if="$auth.isAuthenticated" @click="logout">
          Log out</a>
      </div>
</template>

<script>
export default {
  name: 'Login',
  methods: {
  // Log the user in
    login() {
      this.$auth.loginWithRedirect();
    },
    // Log the user out
    logout() {
      this.$auth.logout({
        returnTo: window.location.origin,
      });
    },
  },
};
</script>

<style lang="scss">

</style>
