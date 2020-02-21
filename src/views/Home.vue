

<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <h1>NEW Place</h1>
    <div>
      Name:
      <input type="text" v-model="newPlaceName">
      Address:
      <input type="text" v-model="newPlaceAddress">
      <button v-on:click="createPlace()">Create Place</button>
    </div>


    <div v-for="place in places">
      <h2>{{place.name}}</h2>
      
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Places App!",
      places: [],
      newPlaceAddress: "",
      newPlaceName: ""
    };
  },
  created: function() {
    axios.get("/api/places").then(response => {
      this.places = response.data;
    });
  },
  methods: {
    createPlace: function() {
      var params = {
        name: this.newPlaceName,
        address: this.newPlaceAddress
      };
      axios.post("api/places", params).then(response => {
        this.places.push(response.data);
        this.newPlaceName = "";
        this.newPlaceAddress = "";


      });

    }
  }
};
</script>
