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
    <a class="submit" @click="addScores" tag="button">Finish</a>
    <Finish
      id="trueSelfDiv"
      v-if="finished"
      :trueSelf="highScore"
    />
  </div>
</template>

<script>
import Question from "../components/question.vue";
import Finish from '../components/finish.vue';
import { questions } from "../data/questions";
import VueSmoothScroll from 'vue2-smooth-scroll'

export default {
  name: "Index",
  components: {
    Question,
    Finish,
    VueSmoothScroll,
  },
  data() {
    return {
      questions,
      scores: {},
      selectedAnswers: {},
      highScore: {},
      finished: false,
    };
  },
  methods: {
    setPoints({ studentScores, questionNum }) {
      // Add question num and scores to dict
      this.selectedAnswers[questionNum.toString()] = studentScores;
    },

    addScores() {
      // If all questions haven't been answered, don't submit
      if (Object.keys(this.selectedAnswers).length !== this.questions.length){
        return
      }

      this.$router.push("#trueSelfDiv");

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
      this.highScore = { name: "", val: 0 };
      Object.keys(this.scores).forEach((student) => {
        const score = this.scores[student];
        if (score > this.highScore.val) {
          this.highScore.name = student;
          this.highScore.val = score;
        }
      });
      this.finished = true;

      console.log(
        `Highest score: ${this.highScore.name}. Points: ${this.highScore.val}`
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
  padding: 5px 10px 5px 10px;
  margin-bottom: 60px;
}

.header {
  margin-bottom: 50px;
}
</style>
