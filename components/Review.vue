<template>
  <div class="review-component-div">
    <div class="review-upper">
      <div class="review-id">
        <span class="pretext">Review ID: </span>{{ revid }}
      </div>
      <div class="review-name">
        <span class="pretext">Submitted By: </span>{{ reviewername }}
      </div>
    </div>
    <div class="review-lower">
      <div class="review-val">{{ revval }}</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "review",
  props: {
    revid: String,
    revval: String,
    reviewername: String,
  },
};
</script>
<style scoped>
.review-component-div {
  display: flex;
  flex-direction: column;
  width: 90%;
  border-radius: 0.5rem;
  border: 1px solid black;
  margin-bottom: 1rem;
  padding: 0.5rem;
  box-shadow: 1px 5px 1rem teal;
  box-shadow: blur(1rem);
  color: white;
}
.review-upper {
  display: flex;
  justify-content: space-between;
}
.review-id,
.review-name {
  flex-basis: 50%;
}
.pretext {
  font-weight: bold;
  color: blueviolet;
}
.review-val {
  text-align: center;
  color: white;
  font-weight: bold;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  font-size: 1.5rem;
}
</style>
