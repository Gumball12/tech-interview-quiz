<template>
  <section>
    <quiz-card v-if="!isAllLoad" :title-raw="randomData[0]" :answer-raw="randomData[1]" />

    <template v-else>
      <quiz-card
        v-for="([title, answer], ind) in data"
        :key="ind"
        :title-raw="title"
        :answer-raw="answer"
      />
    </template>
  </section>
</template>

<script>
import yaml from 'yaml';

import QuizCard from './QuizCard.vue';

const base = process.env.NODE_ENV === 'production' ? 'https://raw.githubusercontent.com/Gumball12/tech-interview-quiz-items/master' : '';

async function recursiveImport(raw) {
  const importStmts = raw.match(/^-\s*?\${.*?}$/gm);

  if (importStmts === null) {
    return raw;
  }

  // eslint-disable-next-line no-restricted-syntax
  for (const importStmt of importStmts) {
    const uri = importStmt.match(/\${(.*?)}/)[1];
    const importSrc = `${base}${uri}`;
    // eslint-disable-next-line no-await-in-loop
    const importRaw = await (await fetch(importSrc)).text();

    // eslint-disable-next-line no-param-reassign
    raw = raw.replace(importStmt, importRaw);
  }

  return recursiveImport(raw);
}

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
    // eslint-disable-next-line
    const srcRaw = '- ${/quiz.yml}';
    const raw = await recursiveImport(srcRaw);
    this.data = yaml.parse(raw);
  },
};
</script>
