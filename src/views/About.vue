<template>
<div class="container">
  <div class="about">
    <h3 class="title">This is an about page</h3>
    <p>There’s a cool little service, <a href="https://eu.ui-avatars.com/">UI Avatars</a>, that lets you generate
      avatars with initials from names on the fly without any kind of backend process.
      It has a simple-to-use API.<br>
      The goal of the app I build is to let a user enter name or surname, or both,
      and then press a button that generates the avatar. More customization options are
      also available.<br>
      To make it a little more complicated, I would add user authorisation in case if user
      wants to keep a history of all the avatars he has generated.</p>
       <h4>Technologies used:</h4>
      <div class="technologies">
        <div class="card">
          <img src="https://upload.wikimedia.org/wikipedia/commons/9/95/Vue.js_Logo_2.svg"/>
          <p>Vue</p>
        </div>
         <div class="card">
          <img src="https://seeklogo.com/images/F/firebase-logo-402F407EE0-seeklogo.com.png"/>
          <p>Firebase</p>
        </div>
         <div class="card">
          <img src="https://miro.medium.com/max/3840/1*Y4XYHylpigYOvfeqGWQmiQ.png"/>
          <p>Axios</p>
        </div>
         <div class="card">
          <img src="https://cdn.freebiesupply.com/logos/thumbs/2x/auth0-logo.png"/>
          <p>Auth0</p>
        </div>
      </div>
  </div>
  </div>
</template>

<script>
</script>

<style lang="scss">
  .about{
    max-width: 800px;
  }
  .container{
    margin-top: 50px;
    display: flex;
    justify-content: center;
  }
  .title{
    font-size: 29px;
    color:#1fbc9c;
    text-shadow: -4px -4px 10px rgba(255, 254, 255, 0.6), 0.7px 1px 1px
     rgba(35, 64, 94, 0.075), 3.5px 5px 3px
     rgba(35, 64, 94, 0.06), 6.3px 9px 5px rgba(35, 64, 94, 0.055), 9.1px 13px 7px
     rgba(35, 64, 94, 0.05), 11.9px 17px 9px rgba(35, 64, 94, 0.05);
  }
  .technologies{
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
  }
  .card{
    display: flex;
    padding: 15px;
    box-shadow: -2px -2px 5px #FFF, 2px 2px 5px  #BABECC;
    margin: 10px;
    width: 100px;
    flex-direction: column;
    text-align: center;
  }
  .card > img{
    height: 87px;
  }
</style>
