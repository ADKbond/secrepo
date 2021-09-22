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
    <Modaltest
      :togglevar="toggler"
      @modalclosefunc="modalclosefunc"
      :tempUserData="tempUserData"
      :peopleData="peopleData"
    />
    <!-- <div class="modal-div">
      <b-modal centered id="modal-center">
        <div class="modal-data-div">
          <img
            :src="tempUserData.imgurl"
            alt=""
            :class="
              tempUserData.gender === 'male'
                ? 'modal-img border-male'
                : 'modal-img border-female'
            "
          />
          <div class="modal-name-text font-primary">
            {{ tempUserData.fname }} {{ tempUserData.lname }}
          </div>
          <div class="modal-mail-div font-secondary">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-envelope-open-fill"
              viewBox="0 0 16 16"
            >
              <path
                d="M8.941.435a2 2 0 0 0-1.882 0l-6 3.2A2 2 0 0 0 0 5.4v.313l6.709 3.933L8 8.928l1.291.717L16 5.715V5.4a2 2 0 0 0-1.059-1.765l-6-3.2zM16 6.873l-5.693 3.337L16 13.372v-6.5zm-.059 7.611L8 10.072.059 14.484A2 2 0 0 0 2 16h12a2 2 0 0 0 1.941-1.516zM0 13.373l5.693-3.163L0 6.873v6.5z"
              />
            </svg>
            {{ tempUserData.email }}
          </div>
          <div class="address-div">
            <h1 class="font-primary">
              Address
            </h1>
            <span
              >{{ tempUserData.city }},{{ tempUserData.state }},{{
                tempUserData.country
              }}</span
            >
          </div>
          <div class="modal-review-div">
            <div v-for="revs in tempUserData.rev" :key="revs.revid">
              <Review :revs="revs.val" />
            </div>
          </div>
          <div class="review-form">
            <input type="text" class="person-review" />
            <b-button
              @click="submitrev(tempUserData.uid)"
              variant="primary"
              class="review-btn"
              >Submit Review
            </b-button>
          </div>
        </div>
      </b-modal>
    </div> -->
  </div>
</template>
<script>
export default {
  name: "homepage",
  data() {
    return {
      peopleData: [],
      tempUserData: {},
      modalShow: false,
      toggler: false
    };
  },
  updated() {
    document.querySelector(".show-people-div").scrollTo({
      top: document.querySelector(".show-people-div").scrollHeight,
      behavior: "smooth"
    });

    console.log("UPDATED and the modalShowvalue is ->", this.modalShow);
  },
  methods: {
    modalclosefunc(val) {
      console.log("EMITTED CLOSER FUNCTION", val);
      this.toggler = val;
    },
    emittedpeopledata(data, val) {
      console.log("DATA", data);
      this.peopleData = this.peopleData.concat(data);
      if (val) {
        this.toggler = val;
      }
      console.log("PEOPES", this.peopleData);
    },
    openModal(dat, val) {
      console.log("Modal Data-------------->", dat);
      this.tempUserData = dat;
      if (val) {
        this.toggler = val;
      }
      console.log("TOGGLER VALUE", val);
      this.modalShow = !this.modalShow;
    }
    //ENTER SUBMIT REV IF SOMETHING GOES WRONG WITH MODAL
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
.modal-data-div {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.modal-img {
  border-radius: 50%;
}
.border-male {
  border: 5px solid skyblue;
}
.border-female {
  border: 5px solid rgb(238, 142, 190);
}
.address-div {
  width: 100%;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.modal-review-div {
  width: 100%;
}
.font-primary {
  font-weight: bold;
  font-size: 2rem;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}
.font-secondary {
  font-weight: bold;
  font-size: 1rem;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}
</style>
