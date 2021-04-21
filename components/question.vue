<template>
  <div class="header">
    <div>
      <h1>
        Question {{ questionNum }}
      </h1>
      <h2>{{ title }}</h2>
      <div v-for="(answer, index) in Object.keys(answers)" :key="index">
        <button @click="passPoints(answers[answer], questionNum)">{{ answer }}</button>
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
      answers: Object,
  },
  data(){
    return {
      mySVG: require('../assets/images/logo.svg')
    }
  },
  methods: {
    passPoints(studentScores, questionNum) {
      this.$emit('setPoints', { studentScores, questionNum });
    }
  }

};
</script>

<style>
button {
  border-style: none;
  margin-top: 10px;
  background-color: red;
  color: white;
}
</style>
