/* People cards */

<template>
  <!-- Image of the close X -->
  <div @mouseover="showXf" @mouseleave="hideXf">
    <hr />
    <img
      @click="deleteCard"
      v-if="showX"
      class="x"
      src="https://www.flaticon.com/svg/static/icons/svg/169/169242.svg"
      alt=""
    />
    <!-- Information about the contact -->
    <h4>Name: {{ client.name | upperCaseProcessing }}</h4>
    <p>Email: {{ client.email }}</p>
    <p>Description: {{ client.description }}</p>

    <!-- This line was to change the card color in order to give a premium version -->
    <!--  <b-button @click="changeColor($event)" type="is-primary">{{buttomColorText}}</b-button>
    -->
    <hr />
  </div>
</template>

<script>
export default {
  data() {
    return {
      /* ifPremium: false,
      buttomColorText: "Change color to premium", */

      /* variable to control x display */
      showX: false,
    };
  },
  props: {
    /* What is reciven from APP.vue, in this case the contact object */
    client: Object,
  },

  methods: {
    /* changeColor: function ($event) {
      console.log($event);
      if (this.ifPremium == false) {
        this.ifPremium = true;
        this.buttomColorText = "Change color to basic";
      } else {
        this.ifPremium = false;
        this.buttomColorText = "Change color to premium";
      }
    }, */

    /* x controllers */
    showXf: function () {
      this.showX = true;
    },
    hideXf: function () {
      this.showX = false;
    },
    /* delete card function */
    deleteCard: function () {
      this.$emit("deleteCardX", { id: this.client.id, component: this });
    },
  },
  /* Uper casing names */
  filters: {
    upperCaseProcessing: function (value) {
      return value.toUpperCase();
    },
  },
  /* This is not being used, but is an exemple of computed elements */
  computed: {
    specialID: function () {
      return this.client.email + this.client.name;
    },
  },
};
</script>

<style scoped>
/* x css */
.x {
  max-width: 20px;
  margin-left: 90%;
}
</style>