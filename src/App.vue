/*
 Thank you for checking my project!

This is a simple Vue.js app
this is my first vue js project and,
thanks to my previous JS knowledge, I found vue.js 
quite intuitive. I recomend you to explore the 
project and read the comments I left for full
 understand the mechanics behind it.
 */


<template >
  <div id="app">
    <!-- call and setup of background particules -->
    <vue-particles
      color="#7B1FA2"
      :particleOpacity="0.9"
      :particlesNumber="120"
      shapeType="polygon"
      :particleSize="3"
      linesColor="#00acd6"
      :linesWidth="1"
      :lineLinked="true"
      :lineOpacity="0.4"
      :linesDistance="100"
      :moveSpeed="2"
      :hoverEffect="true"
      hoverMode="grab"
      :clickEffect="true"
      clickMode="repulse"
    >
    </vue-particles>
    <div>
      <h3>Contact List</h3>
      <!-- contact form -->
      <b-input type="text" placeholder="name" v-model="nameField" /><br />
      <b-input type="text" placeholder="email" v-model="emailField" /><br />
      <b-input
        type="text"
        placeholder="description"
        v-model="descriptionField"
      />
      <br />
      <b-button @click="addClient">Add</b-button>
      <hr />
    </div>
    <!-- Caling all contact cards -->
    <div v-for="client in orderClients" :key="client.id">
      <!-- Caling Contact component -->
      <Client :client="client" @deleteCardX="deleteCard($event)" />
    </div>

    <h2>Credits</h2>
    <!-- Caling Footer component -->
    <Footer />
  </div>
</template>

<script>
/* Imports */
import Client from "./components/Client";
import Footer from "./components/Footer";
/* Library lodash */
import _ from "lodash";

export default {
  name: "App",
  /* Internal varaibles */
  data() {
    return {
      nameField: "",
      emailField: "",
      descriptionField: "",
      /* clients array */
      clients: [],
    };
  },
  /* methods  */
  methods: {
    /* method to add new client to clients array */
    addClient: function () {
      /* small validation use as an example */
      if (this.nameField.length < 3) {
        /* Small alert */
        alert("Invalid name");
      } else {
        /* creating the object into the array */
        this.clients.push({
          id: Date.now(),
          name: this.nameField,
          email: this.emailField,
          description: this.descriptionField,
        });
        this.descriptionField = "";
        this.nameField = "";
        this.emailField = "";
      }
    },
    /* Function to delete event */
    deleteCard: function ($event) {
      /* reciving data from Contact component */
      var id = $event.id;
      /* Creating a new array */
      var newArray = this.clients.filter((client) => client.id != id);
      /* replace clients array */
      this.clients = newArray;
    },
  },
  /* computed functions */
  computed: {
    /* Order clients by name */
    orderClients: function () {
      /* using lodash library */
      return _.orderBy(this.clients, ["name"], ["asc"]);
    },
  },
  /* defining the components */
  components: {
    Client,
    Footer,
  },
};
</script>

<style>
/* The default global css is import from Beufy framework */

/* Aligning content inside body */
body {
  text-align: center;
}
/* styling input boxes */
input {
  width: 50% !important;
}
/* Styling dynamic background */
#particles-js {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0px;
  /* Assuring that the background is behind all content */
  z-index: -1;
}
</style>
