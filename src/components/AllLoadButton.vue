<template>
  <section @click="$emit('change')">
    <button>{{ state ? '원래대로' : '모든 문제 보기' }}</button>
  </section>
</template>

<script>
export default {
  props: {
    state: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style scoped>
section {
  position: fixed;
  right: 1em;
  bottom: 1em;
}
</style>
