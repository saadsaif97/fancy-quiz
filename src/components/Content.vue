<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template slot="lead">
        {{ question.question }}
      </template>
      <hr class="my-4" />
      <b-list-group class="mb-4">
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click="selectAnswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>
      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" class="ml-2" @click="next" href="#"
        >Next</b-button
      >
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  props: {
    question: Object,
    next: Function,
  },
  data() {
    return {
      selectedIndex: Number,
      shuffledAnswers: [],
    };
  },
  watch: {
    question: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.shuffleAnswers();
      },
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
      console.log(index);
    },
    shuffleAnswers() {
      let answers = [
        ...this.question.incorrect_answers,
        this.question.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(answers);
    },
  },
  computed: {
    answers() {
      let answers = [...this.question.incorrect_answers];
      answers.push(this.question.correct_answer);
      return answers;
    },
  },
  mounted() {
    this.shuffleAnswers();
  },
};
</script>

<style scoped>
.list-group-item:hover {
  background-color: #e9e9e9;
}
.selected {
  background-color: lightgoldenrodyellow;
}
.selected:hover {
  background-color: lightgoldenrodyellow;
}
</style>
