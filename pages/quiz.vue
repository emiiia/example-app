<template>
  <div class="header">
    <div v-for="(q, index) in questions" :key="index">
      <Question :questionNum="index + 1" :title="q.title" :answers="q.answers" @setPoints="setPoints" />
    </div>
    <button class="submit" @click="addScores">Submit Answers</button>
  </div>
</template>

<script>
import Question from '../components/question.vue';
import { questions } from '../data/questions'

export default {
  name: 'Index',
  components: {
    Question,
  },
  data(){
    return {
      questions,
      scores: {
        'Emilia': 0,
        'Charlie': 0,
        'Sarah': 0,
        'Jobie': 0,
        'Ellie': 0,
        'Casey': 0,
        'Dulcie': 0,
        'Jacob': 0,
        'Ollie': 0,
        'Rosie': 0,
        'Emily': 0,
        'Abi': 0,
        'Rasneet': 0,
        'Aleeza': 0,
        'Ikhra': 0,
      },
      selectedAnswers: {
      },
    }
  },
  methods: {
    setPoints({ studentScores, questionNum }) {
      this.selectedAnswers[questionNum.toString()] = studentScores;
      console.log(this.selectedAnswers)
    },
    addScores(){
      Object.values(this.selectedAnswers).forEach((studentScores) =>  {
        Object.keys(studentScores).forEach((student) =>  {
          const score = studentScores[student]
          this.scores[student] += score;
        });
      });

      const highScore = { name: '', val: 0 };
      Object.keys(this.scores).forEach((student) =>  {
        const score = this.scores[student]
        if (score > highScore['val']) {
          highScore['name'] = student;
          highScore['val'] = score;
        }
      });
      
      console.log(`Highest score: ${highScore['name']}. Points: ${highScore['val']}`);
    },
  },
};
</script>

<style scoped>
.submit {
  margin-top: 50px;
  background-color: black;
}
</style>
