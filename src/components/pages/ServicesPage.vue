<template>
  <v-container fluid>
    <p>Choose Services</p>
    <v-checkbox
      v-model="selected"
      label="Apartments"
      value="Apartments"
    ></v-checkbox>
    <v-checkbox v-model="selected" label="Hotels" value="Hotels"></v-checkbox>
    <v-checkbox
      v-model="selected"
      label="Restaurants"
      value="Restaurants"
    ></v-checkbox>
    <v-checkbox v-model="selected" label="Tours" value="Tours"></v-checkbox>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      selected: [''],
    };
  },
};
</script>

<style></style>
