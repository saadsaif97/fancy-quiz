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
          :class="addClass(index)"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>
      <b-button
        variant="primary"
        @click="submit"
        :disabled="!selected || submitted"
        >Submit
      </b-button>
      <b-button variant="success" class="ml-2" @click="next" :disabled="last"
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
    check: Function,
    last: Boolean,
  },
  data() {
    return {
      selectedIndex: Number,
      shuffledAnswers: [],
      selected: false,
      submitted: false,
      correctIndex: Number,
    };
  },
  watch: {
    question: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.shuffleAnswers();
        this.selected = null;
        this.submitted = null;
        this.correctIndex = this.shuffledAnswers.indexOf(
          this.question.correct_answer
        );
        console.log(this.correctIndex);
      },
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
      this.selected = true;
    },
    shuffleAnswers() {
      let answers = [
        ...this.question.incorrect_answers,
        this.question.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(answers);
    },
    submit() {
      this.submitted = true;
      if (this.selectedIndex === this.correctIndex) {
        this.check(true);
      } else {
        this.check(false);
      }
    },
    addClass(index) {
      let listClass = "";
      if (
        this.selected &&
        !this.submitted &&
        !this.submitted &&
        index === this.selectedIndex
      ) {
        listClass = "selected";
      } else if (this.submitted && index === this.correctIndex) {
        listClass = "correct";
      } else if (
        this.submitted &&
        index === this.selectedIndex &&
        this.selectedIndex !== this.correctIndex
      ) {
        listClass = "incorrect";
      }

      return listClass;
    },
  },
  computed: {
    answers() {
      let answers = [...this.question.incorrect_answers];
      answers.push(this.question.correct_answer);
      return answers;
    },
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
.correct {
  background-color: rgb(46, 179, 90);
  color: #fff;
}
.incorrect {
  background-color: rgb(255, 113, 70);
  color: #fff;
}
</style>
