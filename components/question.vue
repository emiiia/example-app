<template>
  <div class="header">
    <div>
      <div class="question">
        <h2>{{ title }}</h2>
      </div>
      <div class="answers-container">
        <div
          class="answers"
          v-for="(answer, answerNum) in Object.keys(answers)"
          :key="answerNum"
        >
          <img
            :src="getImgUrl(answers[answer].image)"
            :class="
              selected == answerNum.toString()
                ? 'btn-selected btn-img'
                : 'btn-img'
            "
            @click="passPoints(answers[answer].scores, questionNum, answerNum)"
          />
          <div class="answer-title">
            {{ answer }}
          </div>
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
.question {
  margin: auto;
  background-color: darkcyan;
  width: 70%;
  min-height: 100px;
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: column;
  margin-bottom: 60px;
}

.question h2 {
  color: white;
  font: italic bold 60px Arial;
}

.answers-container {
  margin: auto;
}
.answers {
  display: inline-block;
  padding: 40px;
}

.answer-title {
  padding-top: 40px;
  font: bold 24px Arial;
}

.btn-img {
  width: 300px;
  height: 300px;
  border: 5px solid #555;
}

.btn-selected {
  border: 5px solid goldenrod;
}
</style>
