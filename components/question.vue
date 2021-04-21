<template>
  <div class="header">
    <div>
      <h1>Question {{ questionNum }}</h1>
      <h2>{{ title }}</h2>
      <div class="answers-container">
        <div class="answers" v-for="(answer, answerNum) in Object.keys(answers)" :key="answerNum">
          <img
            :src="getImgUrl(answers[answer].image)"
            :class="selected == answerNum.toString() ? 'btn-selected btn-img' : 'btn-img'"
            @click="passPoints(answers[answer].scores, questionNum, answerNum)"
          />
        </div>
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
      selected: "",
    };
  },
  methods: {
    passPoints(studentScores, questionNum, answerNum) {
      // Update selected answer
      this.selected = answerNum.toString();
      // Pass scores to parent
      this.$emit("setPoints", { studentScores, questionNum });
    },
    getImgUrl(url) {
      if (url) {
        return require("../assets/images/" + url);
      }
    },
  },
};
</script>

<style>
.btn-img {
  width: 200px;
  height: 200px;
  border: 5px solid #555;
}
.btn-selected {
  border: 5px solid red;
}
.answers-container {
  display: flex;
}
.answers {
  flex: 25%;
  padding: 5px;
}
</style>
