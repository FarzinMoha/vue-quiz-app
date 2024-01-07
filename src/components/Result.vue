<script setup>
import { computed } from "vue";
const { answeredCorrect, results } = defineProps([
  "answeredCorrect",
  "results",
]);

const resultIndex = computed(() => {
  let index = 0;

  results.forEach((item, i) => {
    if (item.min <= answeredCorrect && item.max >= answeredCorrect) {
      index = i;
    }
  });

  return index;
});
</script>

<template>
  <div class="result">
    <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">
      {{ results[resultIndex].desc }}
    </div>
  </div>
</template>
