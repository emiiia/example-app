<template>
  <div class="header">
    <div v-for="(q, index) in questions" :key="index">
      <Question
        :questionNum="index + 1"
        :title="q.title"
        :answers="q.answers"
        @setPoints="setPoints"
      />
    </div>
    <button class="submit" @click="addScores">Finish</button>
  </div>
</template>

<script>
import Question from "../components/question.vue";
import { questions } from "../data/questions";

export default {
  name: "Index",
  components: {
    Question,
  },
  data() {
    return {
      questions,
      scores: {},
      selectedAnswers: {},
    };
  },
  methods: {
    setPoints({ studentScores, questionNum }) {
      // Add question num and scores to dict
      this.selectedAnswers[questionNum.toString()] = studentScores;
      console.log(this.selectedAnswers)
    },

    addScores() {
      // Reset scores
      this.scores = {};
      // Add up all the scores for each answer
      Object.values(this.selectedAnswers).forEach((studentScores) => {
        Object.keys(studentScores).forEach((student) => {
          const score = studentScores[student];
          if (!this.scores[student]) {
          // Add student to scores dict
            this.scores[student] = score;
          } else {
            this.scores[student] += score;
          }
        });
      });

      // Get the highest score
      const highScore = { name: "", val: 0 };
      Object.keys(this.scores).forEach((student) => {
        const score = this.scores[student];
        if (score > highScore.val) {
          highScore.name = student;
          highScore.val = score;
        }
      });

      console.log(
        `Highest score: ${highScore.name}. Points: ${highScore.val}`
      );
    },
  },
};
</script>

<style scoped>
.submit {
  background-color: darksalmon;
  color: white;
  margin: 50px;
  font: italic bold 32px Arial;
  width: 200px;
  height: 50px;
}
</style>
