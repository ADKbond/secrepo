<template>
  <div class="homepage-div">
    <div class="show-people-div">
      <div
        v-for="(data, index) in peopleData"
        :key="index"
        class="show-people-div-in"
      >
        <ShowPeople :data="data" />
      </div>
    </div>

    <div class="people-btn-div">
      <People @emittedpeople="emittedpeopledata" />
    </div>
  </div>
</template>
<script>
export default {
  name: "homepage",
  data() {
    return {
      peopleData: []
    };
  },
  updated() {
    document.querySelector(".show-people-div").scrollTo({
      top: document.querySelector(".show-people-div").scrollHeight,
      behavior: "smooth"
    });

    console.log("UPDATED");
  },
  methods: {
    emittedpeopledata(data) {
      console.log("DATA", data);
      this.peopleData = this.peopleData.concat(data);
      console.log("PEOPES", this.peopleData);
    }
  }
};
</script>
<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
:root {
  font-size: 0.875em;
}
.homepage-div {
  display: flex;
  flex-direction: column;
  height: 100vh;
  /* width: 100vw; */
}
.show-people-div {
  flex-basis: 80%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  overflow-y: scroll;
}
.people-btn-div {
  flex-basis: 20%;
}
.show-people-div-in {
  flex-basis: 20%;
}
</style>
