<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="6" md="3">
        <v-text-field v-model="search" label="Search" outlined></v-text-field>
      </v-col>
      <v-col>
        <v-btn @click="searchData()">Search</v-btn>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col  align-self="center" v-if="loading" >
        <div class="d-flex justify-center">
       <v-progress-circular indeterminate color="primary" />
       </div>
      </v-col>
      <v-col v-else v-for="(item, index) in photos" v-bind:key="index">
        <card :data="item" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import card from "./Card";
import axios from "axios";
export default {
  data: () => ({
    search: "",
    photos: "",
    loading: true,
    photodata: "",
  }),
  components: {
    card,
  },
  methods: {
    fecthData() {
      this.loading = true;
      axios
        .get(
          "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=p1v9iusZJSsWsj5taNVjJIfAGOg9mdzezScnD7G1&fbclid=IwAR2ELljNBooebWE-Wxr09YjVnqZKCSLCjn8bAYPTW-DkUWY0pwF8BHo9SJg"
        )
        .then((res) => {
          this.photos = res.data.photos;
          this.photodata = res.data.photos;
          this.loading = false;
        });
    },
    searchData() {
      this.photos = [];
      var full_name = this.photodata.filter(
        (obj) => obj.camera.full_name === this.search
      );
      var name = this.photodata.filter(
        (obj) => obj.camera.name === this.search
      );
      var status = this.photodata.filter(
        (obj) => obj.rover.status === this.search
      );
      var i = 0;
      for (i = 0; i < full_name.length; i++) {
        this.photos.push(full_name[i]);
      }
      for (i = 0; i < name.length; i++) {
        this.photos.push(name[i]);
      }
      for (i = 0; i < status.length; i++) {
        this.photos.push(status[i]);
      }
    },
  },
  created() {
    this.fecthData();
  },
  updated() {
    if (this.search == "") {
      this.photos = this.photodata;
    }
  },
};
</script>

<style>
</style>