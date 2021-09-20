<template>
  <div class="homepage-div">
    <div class="show-people-div">
      <div
        v-for="(data, index) in peopleData"
        :key="index"
        class="show-people-div-in"
      >
        <ShowPeople :data="data" @openModal="openModal" />
      </div>
    </div>

    <div class="people-btn-div">
      <People @emittedpeople="emittedpeopledata" />
    </div>
    <div class="modal-div">
      <b-modal v-model="modalShow" centered id="modal-center">
        <h1>{{ tempUserData.fname }}</h1>
        <h1>{{ tempUserData.lname }}</h1>
      </b-modal>
    </div>
  </div>
</template>
<script>
export default {
  name: "homepage",
  data() {
    return {
      peopleData: [],
      tempUserData: {},
      modalShow: false
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
    },
    showMsgBoxOne() {
      this.boxOne = "";
      this.$bvModal
        .msgBoxOk("Action completed")
        .then(value => {
          this.boxOne = value;
        })
        .catch(err => {
          // An error occurred
        });
    },
    openModal(dat) {
      console.log("Modal Data-------------->", dat);
      this.tempUserData = dat;
      this.modalShow = !this.modalShow;
      console.log(this.tempUserData);
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
.modal-content {
  height: 50rem;
}

.fade {
  backdrop-filter: blur(1rem);
}
</style>
