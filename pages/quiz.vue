<template>
  <div class="header">
    <div v-for="(q, index) in questions" :key="index">
      <Question :questionNum="index + 1" :title="q.title" :answers="q.answers" />
    </div>
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
    }
  }
};
</script>

