<template>
  <div class="app">
    <main>
      <quiz-card />
      <info-msg />
    </main>
  </div>
</template>

<script>
import QuizCard from './components/QuizCard.vue';
import InfoMsg from './components/InfoMsg.vue';

export default {
  name: 'App',
  components: {
    QuizCard,
    InfoMsg,
  },
};
</script>

<style>
@import url(//fonts.googleapis.com/earlyaccess/jejugothic.css);

* {
 font-family: 'Jeju Gothic', sans-serif;
}

html, body {
  height: 100%;
  margin: 0;
}
</style>

<style scoped>
div.app {
  height: 100%;
  background-color: #fafafa;
}

main {
  display: flex;
  flex-direction: column;
  justify-content: center;

  min-height: 100%;
}
</style>
