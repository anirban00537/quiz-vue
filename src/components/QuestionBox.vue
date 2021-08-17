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
          @click.prevent="selectAnswer(index)"
          :class="answerClass(index)"
        >
          {{ answer }}</b-list-group-item
        >
      </b-list-group>

      <b-button
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
        >Submit</b-button
      >
      <b-button variant="success" href="#" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  props: {
    questions: Object,
    next: Function,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      suffledAnswers: [],
      correctIndex: null,
      answered: false,
    };
  },
  watch: {
    questions() {
      this.selectedIndex = null;
      this.answered = false;
      this.suffledtAnswers();
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }

      this.answered = true;
      this.increment(isCorrect);
    },
    answerClass(index) {
      let ansClass = "";

      if (!this.answered && this.selectedIndex == index) {
        ansClass = "selected";
      } else if (this.answered && this.correctIndex == index) {
        ansClass = "correct";
      } else if (
        this.answered &&
        this.selectedIndex == index &&
        this.correctIndex !== index
      ) {
        ansClass = "incorrect";
      } else {
        ansClass = "";
      }
      return ansClass;
    },

    suffledtAnswers() {
      let answers = [
        ...this.questions.incorrect_answers,
        this.questions.correct_answer,
      ];
      this.suffledAnswers = _.shuffle(answers);
      this.correctIndex = this.suffledAnswers.indexOf(
        this.questions.correct_answer
      );
    },
  },
  mounted() {
    this.suffledtAnswers();
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
.selected {
  background-color: #00bcd4;
}
.correct {
  background-color: green;
}
.incorrect {
  background-color: red;
}
</style>
