<template>
  <div id="app">
    <AppHeader />
    <main id="main">
      <HomeView></HomeView>
    </main>
    <AppFooter />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader';
import AppFooter from './components/AppFooter.vue';
import HomeView from './components/HomeView.vue';


export default {
  name: 'App',
  components: {
    AppHeader,
    AppFooter,
    HomeView,
  }
}

</script>


<style>


*{
  box-sizing: border-box;
}

body, ul, li, h1, h2, p{
  margin: 0px;
  padding: 0px;
}

ul{
  list-style: none;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  color: #345;
}

a{
  color: #345;
  text-decoration: none;
}

img{
  max-width: 100%;
  display: block;
}

#app{
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

#main{
  flex: 1;
  background: black;
}

</style>
