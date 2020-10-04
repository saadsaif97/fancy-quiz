<template>
  <div id="app">
    <Header :number="index" />
    <b-container class="my-5">
      <b-row>
        <b-col sm="10" offset-sm="1" md="8" offset-md="2" lg="6" offset-lg="3">
          <Content
            :question="questions[index]"
            :next="next"
            v-if="questions.length"
            :last="index === 9 ? true : false"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";

export default {
  name: "App",
  components: {
    Header,
    Content,
  },
  data() {
    return {
      questions: [],
      index: 0,
      last: Boolean,
    };
  },
  methods: {
    next() {
      this.index++;
    },
  },
  mounted() {
    fetch("https://opentdb.com/api.php?amount=10&category=27", {
      method: "get",
    })
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.questions = data.results;
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
