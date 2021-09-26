<template>
  <div class="people-div-1">
    <div>
      <b-card
        :title="data.fname"
        :img-src="data.imgurl"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem"
        class="mb-2"
      >
        <b-card-text>
          {{ data.email }}
        </b-card-text>
        <div class="b-button-div">
          <b-button href="#" variant="primary" @click="openModal($event)"
            >More Details
          </b-button>
          <b-button href="#" variant="danger" @click="deleteFunc(data.uid)"
            >Delete
          </b-button>
        </div>
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
    data: Object,
  },
  data() {
    return {
      modalopenvar: false,
    };
  },
  methods: {
    openModal(e) {
      this.$emit("openModal", this.data, true);
      console.log("HELLLOOOOO", this.data);
    },
    deleteFunc(id) {
      this.$emit("deleteItem", id);
      console.log("DEL IDDDD===>", id);
    },
  },
};
</script>
<style scoped>
.people-div-1 {
  display: flex;
  justify-content: center;
  margin: 1rem;
}
.card:hover {
  z-index: 3;
  transform: scale(1.13, 1.13);
}
.card {
  width: 15rem;
  height: 22rem;
  background: teal;
  box-shadow: 0px 5px 5px black;
  transition: transform 0.5s ease-in-out;
  z-index: 1;
}
.card-img-top {
  height: 10rem;
  width: 15rem;
  padding: 0.5rem;
  margin: 0;
}
.card-body {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.card-title {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-weight: bold;

  text-overflow: ellipsis;
}
.card-text {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  height: 2rem;
  text-overflow: clip;
  font-size: 0.9rem;
}
p.card-text {
  text-overflow: clip;
  height: 2rem;
}
.b-button-div {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  text-overflow: ellipsis;
}
.btn {
  margin: 0.2rem;
}
</style>
