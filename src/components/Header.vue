<template>
  <div>
    <b-nav>
      <b-nav-item disabled tab>Fancy Quiz App</b-nav-item>
      <b-nav-item disabled tab
        >Counter:{{ numCorrect }}/{{ numTotal }}</b-nav-item
      >
    </b-nav>
  </div>
</template>

<script>
export default {
  props: ["numTotal", "numCorrect"],
};
</script>

<style></style>
