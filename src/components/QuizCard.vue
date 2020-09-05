<template>
  <article>
    <h1 v-html="title" />

    <div class="button" v-if="!isAnswerOpen">
      <button @click="isAnswerOpen = true">답 확인</button>
    </div>

    <template v-else>
      <hr>

      <div v-html="answer"/>

      <div class="button">
        <button @click="window.location.reload()">다른 문제</button>
      </div>
    </template>
  </article>
</template>

<script>
import MarkdownIt from 'markdown-it';

export default {
  props: ['title-raw', 'answer-raw'],
  data: () => ({
    isAnswerOpen: false,
  }),
  computed: {
    window() {
      return window;
    },
    answer() {
      return new MarkdownIt().render(this.answerRaw || '');
    },
    title() {
      return new MarkdownIt().render(this.titleRaw || '');
    },
  },
};
</script>

<style scoped>
article {
  margin: auto;
  margin-top: 1em;
  margin-bottom: 1em;

  max-width: 660px;

  padding: 16px;
  padding-left: 20px;
  padding-right: 20px;

  border-radius: 5px;

  background-color: #fefefe;
}

article ::v-deep code {
  background: #eee;
  color: #ff7f00;

  padding: 1px;
  padding-left: 2px;
  padding-right: 2px;
}

article div.button {
  width: 100%;
  text-align: right;
}
</style>
