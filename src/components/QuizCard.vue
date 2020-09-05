<template>
  <div class="card">
    <p class="title" v-text="title" />

    <button v-if="!isAnswerOpen"
      @click="isAnswerOpen = true">답 확인</button>

    <template v-else>
      <hr>
      <div v-html="answer_md"/>
      <button @click="window.location.reload()">다른 문제</button>
    </template>
  </div>
</template>

<script>
import yaml from 'yaml';
import MarkdownIt from 'markdown-it';

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
    answer_md() {
      return new MarkdownIt().render(this.answer);
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
    const data = yaml.parse(raw);
    const randomData = getRandomElement(data);

    [this.title, this.answer] = randomData;
  },
};
</script>

<style scoped>
div.card {
  align-self: center;

  max-width: 660px;

  padding: 16px;
  padding-left: 20px;
  padding-right: 20px;

  border-radius: 5px;

  background-color: #fefefe;
}

div.card > p.title {
  font-size: 32px;
}

div.card button {
  border: none;
  float: right;
  padding: 10px;
  background: transparent;
  text-decoration: underline;
}

div.card button:focus {
  outline: 0;
}
</style>
