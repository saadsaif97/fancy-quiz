<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled><strong>Fancy Quiz App</strong></b-nav-item>
      <b-nav-item disabled>Counter {{ number + 1 }}/10</b-nav-item>
      <b-nav-item disabled>
        <p class="text-success">Correct answers: {{ correct }}</p>
      </b-nav-item>
      <b-nav-item disabled>
        <p class="text-danger">Incorrect answers: {{ inCorrect }}</p>
      </b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: {
    number: Number,
    correct: Number,
    inCorrect: Number,
  },
};
</script>
