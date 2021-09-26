<template>
  <div class="modal-container" @load="changeVal()">
    <div>
      <b-modal ref="my-modal" hide-footer hide-header v-model="togglevar">
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
          <div class="user-detail-div">
            <div class="address-div">
              <h1 class="font-primary detail-title-font">Address:</h1>
              <span class="font-secondary address-font">
                {{ tempUserData.city }} , {{ tempUserData.state }},<br />{{
                  tempUserData.country
                }}</span
              >
            </div>
            <div class="address-div">
              <h1 class="font-primary detail-title-font">Zipcode:</h1>
              <span class="font-secondary address-font">
                {{ tempUserData.postcode }}</span
              >
            </div>
          </div>

          <div class="modal-review-div">
            <div
              v-for="revs in tempUserData.rev"
              :key="revs.revid"
              class="review-for-div"
            >
              <Review
                :revid="revs.revid"
                :reviewername="revs.revname"
                :revval="revs.val"
              />
            </div>
          </div>
          <div class="review-form">
            <input
              type="text"
              class="person-name form-item"
              placeholder="Enter your Name"
            />
            <input
              type="text"
              class="person-review form-item"
              placeholder="Enter your Review"
            />
            <b-button
              @click="submitrev(tempUserData.uid)"
              variant="success"
              class="review-btn form-item"
              >Submit Review
            </b-button>
          </div>
        </div>
      </b-modal>
    </div>
  </div>
</template>
<script>
export default {
  name: "modaltest",
  mounted() {
    // this.$root.$on("bv::modal::show", (bvEvent, modalId) => {
    //   console.log("Modal is about to be shown", bvEvent, modalId);

    // });
    this.$root.$on("bv::modal::hide", (bvEvent, modalId) => {
      console.log("Modal is about to be shown", bvEvent, modalId);
      this.$emit("modalclosefunc", false);
    });
    this.togg = false;
  },
  props: {
    togglevar: Boolean,
    tempUserData: Object,
    peopleData: Array,
  },
  data() {
    return {
      togg: this.togglevar,
    };
  },
  updated() {
    this.togg = this.togglevar;
    console.log("TOGGLERVAR is =>", this.togg);
    if (this.toggler !== "") {
    }
  },
  methods: {
    changeVal() {
      this.togglevar = "load";
      console.log("INNNNNNNNNNNNNN");
    },
    toggleModal() {
      // We pass the ID of the button that we want to return focus to
      // when the modal has hidden  v-model="modalShow"
      this.$refs["my-modal"].toggle();
      console.log("TOGGLE TEST MODAL REACHED");
    },
    submitrev(id) {
      const name = document.querySelector(".person-name").value;
      const val = document.querySelector(".person-review").value;
      if (name === "" || val === "") {
        alert("Please enter a valid Name and Review !");
      } else {
        let s4 = () => {
          return Math.floor((1 + Math.random()) * 0x10000)
            .toString(16)
            .substring(1);
        };

        const x = this.peopleData.filter((people) => {
          if (people.uid === id) {
            people.rev.push({
              revid: s4(),
              revname: name,
              val: val,
            });
            return people;
          }
        });
        console.log("XXXXX", this.peopleData);
      }
    },
  },
};
</script>
<style scoped>
.modal-body {
  background-color: green;
}
.modal-data-div {
  height: 100%;
}
.user-detail-div {
  width: 100%;
  padding: 1rem;
  margin-top: 1rem;
  border: 1px solid lightblue;
}
.address-div {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}
.address-div > h1 {
  flex-basis: 30%;
}
.address-div > span {
  flex-basis: 70%;
}
.address-font {
  font-size: 1.5rem;
}
.review-for-div {
  display: flex;
  justify-content: center;
}
.modal-review-div {
  margin-top: 1rem;
  height: 13rem;
  overflow-y: scroll;
}
.modal-review-div::-webkit-scrollbar {
  display: none;
}
.review-form {
  display: flex;
  width: 100%;
  flex-direction: column;
  justify-content: flex-end;
}

.form-item {
  margin: 0.5rem;
}
.person-name,
.person-review {
  border-radius: 1rem;
  height: 2rem;
  background-color: black;
  color: white;
  font-weight: bold;
  font-family: "Courier New", Courier, monospace;
  border: none;
  box-shadow: none;
  text-align: center;
}
/* .person-name:focus-within,
.person-review:focus {
  border: none;
} */
input:focus {
  outline: none;
}
.detail-title-font {
  color: moccasin;
}
</style>
