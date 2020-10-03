<template>
  <v-card class="mx-auto my-12" max-width="374">
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img height="250" v-bind:src="data.img_src"></v-img>

    <v-card-title>{{ data.camera.name }}</v-card-title>
    <v-card-subtitle>{{ data.camera.full_name }}</v-card-subtitle>
    <v-card-text>
      <div class="my-4 subtitle-1">Camera ID : {{ data.camera.id }}</div>
      <div class="my-4 subtitle-1">Photo ID : {{ data.id }}</div>
      <div class="my-4 subtitle-1">Rover ID : {{ data.rover.id }}</div>
    </v-card-text>

    <v-divider class="mx-4" />
    <v-card-title>Earth Date</v-card-title>
    <v-card-text>
      <v-chip-group active-class="deep-purple accent-4 white--text" column>
        <v-chip>{{ data.earth_date }}</v-chip>
      </v-chip-group>
      <v-divider class="mx-4" />
      <v-card-title>Landing Date</v-card-title>
      <v-chip-group active-class="deep-purple accent-4 white--text" column>
        <v-chip>{{ data.rover.landing_date }}</v-chip>
      </v-chip-group>
      <v-divider class="mx-4" />
      <v-card-title>Launch Date</v-card-title>
      <v-chip-group active-class="deep-purple accent-4 white--text" column>
        <v-chip>{{ data.rover.launch_date }}</v-chip>
      </v-chip-group>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["data"],
};
</script>