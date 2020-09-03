<template>
  <div class="card">
    <p class="title" v-text="title" />

    <button v-if="!isAnswerOpen"
      @click="isAnswerOpen = true">답 확인</button>

    <template v-else>
      <button @click="window.location.reload()">다른 문제</button>
      <p class="answer" v-text="answer"/>
    </template>
  </div>
</template>

<script>
import yaml from 'yaml';

function getRandomElement(arr) {
  const randomIndex = Math.floor(Math.random() * arr.length);
  return arr[randomIndex];
}

export default {
  data: () => ({
    title: '',
    answer: '',
    isAnswerOpen: false,
  }),
  computed: {
    window() {
      return window;
    },
  },
  async mounted() {
    const quizSrc = 'https://raw.githubusercontent.com/Gumball12/tech-interview-quiz-items/master/quiz.yml';

    const raw = await (await fetch(quizSrc)).text();
    const data = yaml.parse(raw);
    const randomData = getRandomElement(data);

    [this.title, this.answer] = randomData;
  },
};
</script>

<style scoped>
div.card {
  align-self: center;

  width: 660px;

  box-shadow: 0px 3px 8px -1px #ccc;

  padding-left: 16px;
  padding-bottom: 12px;
  padding-top: 8px;

  text-align: center;

  border-radius: 3px;
}

div.card > p.title {
  font-size: 32px;
}
</style>
