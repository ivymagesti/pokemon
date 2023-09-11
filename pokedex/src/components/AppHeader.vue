<template>
  <header>
    <nav>
        <img class="logo" src="@/assets/logo.svg" alt="">
 </nav>
  </header>
</template>

<script>

export default {
    name: 'AppHeader'
}

</script>

<style scoped>

nav{
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 15px 20px;
    background: rgb(224, 41, 41);
}

.logo{
    padding: 10px 0;
    max-width: 170px;
}

</style>
