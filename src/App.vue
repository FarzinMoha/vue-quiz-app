<script setup lang="ts">
import { ref } from "vue";
import Result from "./components/Result.vue";
import Question from "./components/Question.vue";
import dataSource from "./data";

const data = ref(dataSource);
const questionAnswered = ref(0);
const answeredCorrect = ref(0);

const answerSelected = (is_correct: boolean) => {
  if (is_correct) {
    answeredCorrect.value++;
  }
  questionAnswered.value++;
};

const reset = () => {
  questionAnswered.value = 0;
  answeredCorrect.value = 0;
};
</script>

<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <Question
        v-if="questionAnswered < data.questions.length"
        :questions="data.questions"
        :questionAnswered="questionAnswered"
        @selectedItem="answerSelected"
      />
      <Result
        v-else
        :results="data.results"
        :answeredCorrect="answeredCorrect"
      />
    </transition>
  </div>
  <button
    v-if="questionAnswered === data.questions.length"
    type="button"
    class="reset-btn"
    @click="reset"
  >
    Reset
  </button>
</template>

<style scoped></style>
