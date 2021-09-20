<template>
  <div class="people-div">
    <button @click="callPeople()">Click Hello to create</button>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "people",
  data() {
    return {
      peoplearr: []
    };
  },
  methods: {
    async callPeople() {
      const people = await axios.get("https://randomuser.me/api/");
      console.log("---->", people.data.results[0]);
      const [fname, lname, email, gender, location, imgurl] = [
        people.data.results[0].name.first,
        people.data.results[0].name.last,
        people.data.results[0].email,
        people.data.results[0].gender,
        people.data.results[0].location.country,
        people.data.results[0].picture.large
      ];
      const data = { fname, lname, email, gender, location, imgurl };
      this.peoplearr = this.peoplearr.concat(data);
      this.$emit("emittedpeople", this.peoplearr[this.peoplearr.length - 1]);
      console.log("=>", this.peoplearr);
    }
  }
};
</script>
<style scoped>
.people-div {
  width: 100%;
  height: 100%;
  background: red;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
