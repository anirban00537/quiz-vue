<template>
  <div id="app">
    <Header />
    <QuestionBox
      v-if="questions.length"
      :questions="questions[index]"
      :next="next"
    />
  </div>
</template>
<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";
export default {
  name: "App",
  components: {
    Header,
    QuestionBox,
  },
  data() {
    return {
      questions: [],
      index: 0,
    };
  },
  methods: {
    next() {
      this.index = this.index + 1;
    },
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&category=22", {
      method: "GET",
    })
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        // console.log(jsonData.results);
        this.questions = jsonData.results;
        console.log(this.questions);
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
