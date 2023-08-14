<template>
  <div>
    <v-row justify="center">
      <v-date-picker v-model="picker" :min="new Date()"></v-date-picker>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      picker: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
    };
  },
};
</script>

<style></style>
