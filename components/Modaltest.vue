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
    peopleData: Array
  },
  data() {
    return {
      togg: this.togglevar
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
      const val = document.querySelector(".person-review").value;
      let s4 = () => {
        return Math.floor((1 + Math.random()) * 0x10000)
          .toString(16)
          .substring(1);
      };
      const x = this.peopleData.filter(people => {
        if (people.uid === id) {
          people.rev.push({
            revid: s4(),
            val: val
          });
          return people;
        }
      });
      console.log("XXXXX", this.peopleData);
    }
  }
};
</script>
<style scoped></style>
