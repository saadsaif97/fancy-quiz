<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled><strong>Fancy Quiz App</strong></b-nav-item>
      <b-nav-item disabled>Counter {{ number }}/10</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: {
    number: Number,
  },
};
</script>
