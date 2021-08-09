<template>
  <div class="question-box-component">
    <b-jumbotron>
      <template #lead>
        {{ questions.question }}
      </template>

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index"
          @click="selectAnswer(index)"
        >
          {{ answer }}</b-list-group-item
        >
      </b-list-group>

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
  data() {
    return {
      selectedIndex: null,
    };
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
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

<style scoped>
.list-group {
  margin: 20px;
}
.list-group-item:hover {
  background-color: black;
  color: white;
}
</style>
