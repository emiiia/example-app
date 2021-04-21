<template>
  <div class="header">
    <div>
      <h1>Question {{ questionNum }}</h1>
      <h2>{{ title }}</h2>
      <div v-for="(answer, answerNum) in Object.keys(answers)" :key="answerNum">
        <button
          :class="selected == answerNum.toString() ? 'btn-selected':''"
          @click="passPoints(answers[answer], questionNum, answerNum)"
        >
          {{ answer }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Question",
  props: {
    questionNum: Number,
    title: String,
    answers: Object,
  },
  data() {
    return {
      mySVG: require("../assets/images/logo.svg"),
      selected: '',
    };
  },
  methods: {
    passPoints(studentScores, questionNum, answerNum) {
      // Update selected answer
      this.selected = answerNum.toString();
      // Pass scores to parent
      this.$emit("setPoints", { studentScores, questionNum });
    },
  },
};
</script>

<style>
button {
  border-style: none;
  margin-top: 10px;
  background-color: red;
  color: white;
}
.btn-selected {
  background-color: pink;
}
</style>
