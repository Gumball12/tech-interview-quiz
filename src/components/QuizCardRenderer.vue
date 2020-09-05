<template>
  <section>
    <quiz-card v-if="!isAllLoad"
      :title-raw="randomData[0]" :answer-raw="randomData[1]" />

    <template v-else>
      <quiz-card v-for="([title, answer], ind) in data" :key="ind"
        :title-raw="title" :answer-raw="answer" />
    </template>
  </section>
</template>

<script>
import yaml from 'yaml';

import QuizCard from './QuizCard.vue';

export default {
  props: {
    isAllLoad: {
      type: Boolean,
      default: false,
    },
  },
  components: { QuizCard },
  data: () => ({
    data: ['', ''],
  }),
  computed: {
    randomData() {
      const randomIndex = Math.floor(Math.random() * this.data.length);
      return this.data[randomIndex];
    },
  },
  async mounted() {
    let quizSrc;

    if (process.env.NODE_ENV === 'production') {
      quizSrc = 'https://raw.githubusercontent.com/Gumball12/tech-interview-quiz-items/master/quiz.yml';
    } else if (process.env.NODE_ENV === 'development') {
      quizSrc = '/quiz.yml';
    }

    const raw = await (await fetch(quizSrc)).text();
    this.data = yaml.parse(raw);
  },
};
</script>
