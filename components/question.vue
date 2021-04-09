<template>
  <div class="header">
    <div>
      <h1>
        Question {{ questionNum }}
      </h1>
      <h2>{{ title }}</h2>
      <div v-for="(answer, index) in answers" :key="index">
        {{ index + 1 }}. {{ answer }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Question',
  props: {
      questionNum: Number,
      title: String,
      answers: Array,
  },
  data(){
    return {
      mySVG: require('../assets/images/logo.svg')
    }
  }
};
</script>

