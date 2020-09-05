<template>
  <div class="app">
    <info-msg />

    <main>
      <quiz-card-renderer :is-all-load="isAllLoad" />
      <all-load-button @change="isAllLoad = !isAllLoad" :state="isAllLoad" />
    </main>
  </div>
</template>

<script>
import QuizCardRenderer from './components/QuizCardRenderer.vue';
import InfoMsg from './components/InfoMsg.vue';
import AllLoadButton from './components/AllLoadButton.vue';

export default {
  name: 'App',
  components: {
    QuizCardRenderer,
    InfoMsg,
    AllLoadButton,
  },
  data: () => ({
    isAllLoad: false,
  }),
};
</script>

<style>
@import url(//fonts.googleapis.com/earlyaccess/jejugothic.css);

* {
 font-family: 'Jeju Gothic', sans-serif;
 line-height: 1.5em;
 word-break: keep-all;
}

html, body {
  height: 100%;
  margin: 0;
}

button {
  border: none;
  padding: 10px;
  background: transparent;
  text-decoration: underline;
}

button:focus {
  outline: 0;
}

hr {
  border: 1px solid #ccc;
  border-bottom: 0;
}
</style>

<style scoped>
div.app {
  height: 100%;
}

main {
  display: flex;
  flex-direction: column;
  justify-content: center;

  min-height: 100%;

  background-color: #fafafa;
}
</style>
