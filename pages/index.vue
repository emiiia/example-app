<template>
  <div class="container">
    <div>
      <img :src="mySVG" />
      <h1 class="title">
        Lilly Students Quiz
      </h1>
      <NuxtLink class="button" to="/quiz">Start Quiz</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Index',
  data(){
    return {
      mySVG: require('../assets/images/logo.svg')
    }
  }
};
</script>