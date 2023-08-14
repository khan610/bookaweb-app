<template>
  <v-container fluid>
    <v-layout align-center justify-center column>
      <h1 class="blue--text text-center">Chose Services</h1>
      <v-layout align-start column>
        <v-checkbox
          v-model="selected"
          label="Apartments"
          value="Apartments"
        ></v-checkbox>
        <v-checkbox
          v-model="selected"
          label="Hotels"
          value="Hotels"
        ></v-checkbox>
        <v-checkbox
          v-model="selected"
          label="Restaurants"
          value="Restaurants"
        ></v-checkbox>
        <v-checkbox v-model="selected" label="Tours" value="Tours"></v-checkbox>
      </v-layout>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      selected: [''],
    };
  },
  methods: {
    emitValues() {
      return this.selected;
    },
  },
};
</script>

<style>
.blue--text {
  color: blue;
  margin-bottom: 20px;
}
.text-center {
  text-align: center;
}
</style>
