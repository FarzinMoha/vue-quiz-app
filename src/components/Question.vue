<script setup>
const { questions, questionAnswered } = defineProps([
  "questions",
  "questionAnswered",
]);
</script>

<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionAnswered / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, index) in questions"
        :key="index"
        v-show="index === questionAnswered"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            class="answer"
            v-for="(answer, index) in question.answers"
            :key="index"
            @click.prevent="$emit('selectedItem', answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>
