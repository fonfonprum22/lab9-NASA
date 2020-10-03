<template>
  <div>
    <v-card
      :to="{
        path: '/Dialog',
        query: { data: `${data.id}` },
        props: { data: `${data.id}` },
      }"
      style="color: hotpink"
      class="mx-auto"
      width="344"
      outlined
    >
      <v-list-item three-line>
        <v-list-item-content>
          <div class="overline mb-4">
            {{ data.camera.full_name }}
          </div>
          <v-list-item-title class="headline mb-1">
            {{ data.camera.name }}
          </v-list-item-title>
          <v-list-item-subtitle>
            {{ data.rover.status }}
          </v-list-item-subtitle>
        </v-list-item-content>

        <v-list-item-avatar tile size="80" color="grey">
          <img class="white--text align-end" v-bind:src="data.img_src" />
        </v-list-item-avatar>
      </v-list-item>
    </v-card>
    <v-dialog v-model="showDialog">
      <dialogData :data="data" />
    </v-dialog>
  </div>
</template>

<script>
import dialogData from "./Dialog";
export default {
  props: ["data"],
  data: () => ({
    showDialog: false,
  }),
  components: {
    dialogData,
  },
};
</script>