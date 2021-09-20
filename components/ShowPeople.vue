<template>
  <div class="people-div-1">
    <div>
      <b-card
        :title="data.fname"
        :img-src="data.imgurl"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem;"
        class="mb-2"
      >
        <b-card-text>
          Some quick example text to build on the card title and make up the
          bulk of the card's content.
        </b-card-text>

        <b-button href="#" variant="primary" @click="openModal()"
          >Go somewhere</b-button
        >
      </b-card>
      <div>
        <!-- <b-button v-b-modal.modal-center>Launch centered modal</b-button> -->
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "showpeople",
  props: {
    data: Object
  },
  data() {
    return {
      userdata: this.data
    };
  },
  methods: {
    openModal() {
      this.$emit("openModal", this.userdata);
      console.log("HELLLOOOOO");
    }
  }
};
</script>
<style scoped>
.people-div-1 {
  display: flex;
  justify-content: center;
}
.card {
  width: 15rem;
  height: auto;
}
.card-img-top {
  height: 10rem;
  width: 15rem;
}
</style>
