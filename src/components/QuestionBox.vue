<template>
  <div class="question-box-component">
    <b-jumbotron>
      <template #lead>
        {{ questions.question }}
      </template>

      <p v-for="(answer, index) in answers" :key="index">
        {{ answer }}
      </p>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" href="#" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: {
    questions: Object,
    next: Function,
  },
  computed: {
    answers() {
      let answers = [...this.questions.incorrect_answers];
      answers.push(this.questions.correct_answer);
      return answers;
    },
  },
};
</script>

<style></style>
