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
          <div
            :class="
              selected == answerNum.toString()
                ? 'img-selected img-container'
                : 'img-container'
            "
          >
            <img
              :src="getImgUrl(answers[answer].image)"
              @click="
                passPoints(answers[answer].scores, questionNum, answerNum)
              "
            />
          </div>
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
  margin: 40px;
}

.img-container {
  overflow: hidden;
  border: 5px solid white;
}

.img-selected {
  border: 5px solid goldenrod;
}

.img-container img {
  display: block;
  transition: transform 0.4s;
  width: 300px;
  height: 300px;
}

.img-container:hover img {
  transform: scale(1.1);
  transform-origin: 50% 50%;
}

.answer-title {
  padding-top: 40px;
  font: bold 24px Arial;
}
</style>
