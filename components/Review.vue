<template>
  <div class="review-component-div">
    <div class="review-revs">{{ revs }}</div>
  </div>
</template>
<script>
export default {
  name: "review",
  props: {
    revs: String
  }
};
</script>
<style scoped>
.review-component-div {
  width: 100%;
  border-radius: 0.5rem;
  border: 1px solid black;
  margin-bottom: 1rem;
  padding: 0.5rem;
  box-shadow: 0px 5px 1rem teal;
  box-shadow: blur(1rem);
}
.review-revs {
  text-align: center;
}
</style>
