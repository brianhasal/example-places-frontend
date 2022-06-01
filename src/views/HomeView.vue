<script>
import axios from 'axios';
  export default {
    data: function () {
      return {
        message: "Chicago Places",
        places: [],
        newPlaceParams: {},
        currentPlace: {},
        showPlaceParams: {}
      };
    },
    created: function () {
      this.indexPlaces();
    },
    methods: {
      indexPlaces: function() {
        axios.get("/places").then((response) => {
          console.log("places index", response);
          this.places = response.data;
        });
      },
      createPlace: function() {
        axios
          .post("/places", this.newPlaceParams)
          .then((response) => {
            console.log("creating place", response);
            this.places.push(response.data);
            this.newPlaceParams = {};
            })
          .catch((error) => {
            console.log("places create error", error.response);
        });

      },
    },
  };
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
      <div>
        Name:
        <input v-model="newPlaceParams.name" type="text">
      </div>
      <div>
        Address:
        <input v-model="newPlaceParams.address" type="text">
      </div>
      <button v-on:click="createPlace()">Create</button>
    </div>
    <div v-for="place in places" v-bind:key="place.id">
      <h1>{{ place.name }}</h1>
      <h2>{{place.address}}</h2>
    </div>
  </div>
</template>

<style></style>