<template>
  <div class="people-div">
    <b-button variant="outline-success" @click="callPeople()"
      >Add a New Person</b-button
    >
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
      const [
        uid,
        fname,
        lname,
        email,
        gender,
        country,
        state,
        city,
        postcode,
        imgurl,
        phone,
        rev
      ] = [
        people.data.results[0].login.uuid,
        people.data.results[0].name.first,
        people.data.results[0].name.last,
        people.data.results[0].email,
        people.data.results[0].gender,
        people.data.results[0].location.country,
        people.data.results[0].location.state,
        people.data.results[0].location.city,
        people.data.results[0].location.postcode,
        people.data.results[0].picture.large,
        people.data.results[0].phone,
        Array()
      ];
      const data = {
        uid,
        fname,
        lname,
        email,
        gender,
        country,
        state,
        city,
        postcode,
        imgurl,
        phone,
        rev
      };
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
  display: flex;
  background: darkslategray;
  justify-content: center;
  align-items: center;
  box-shadow: 5px 0px 5px black;
}
.btn {
  height: 5rem;
  font-size: 2rem;
  border-radius: 1rem;
}
</style>
