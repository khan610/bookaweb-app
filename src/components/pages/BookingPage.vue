<template>
  <v-container fluid>
    <v-layout justify-center align-center>
      <v-flex xs12 md6>
        <v-layout column align-center>
          <h1 class="blue--text">Check-In</h1>
          <v-date-picker
            v-model="checkInDate"
            color="primary"
            :min="minCheckInDate"
            @change="getMinCheckOutDate"
          ></v-date-picker>
        </v-layout>
      </v-flex>
      <v-flex xs12 md6>
        <v-layout column align-center>
          <h1 class="blue--text">Check-Out</h1>
          <v-date-picker
            v-model="checkOutDate"
            color="primary"
            :min="minCheckOutDate"
          ></v-date-picker>
        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      checkInDate: this.getDefaultDate(),
      minCheckInDate: this.getDefaultDate(),
      checkOutDate: '',
      minCheckOutDate: this.getDefaultDate(true),
    };
  },

  methods: {
    getDefaultDate(value = false) {
      if (value) {
        const currentDay = new Date().getDate();
        const checkOutDate = new Date();
        checkOutDate.setDate(currentDay + 1);

        return checkOutDate.toISOString().substr(0, 10);
      } else {
        return new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
          .toISOString()
          .substr(0, 10);
      }
    },

    getMinCheckOutDate() {
      const currentDay = new Date(this.checkInDate).getDate();
      const checkOutDate = new Date(this.checkInDate);
      checkOutDate.setDate(currentDay + 1);
      this.minCheckOutDate = checkOutDate.toISOString().substr(0, 10);

      this.checkIfShouldClearCheckOutDate();
    },

    checkIfShouldClearCheckOutDate() {
      const checkInDate = new Date(this.checkInDate);
      const checkOutDate = new Date(this.checkOutDate);

      if (checkInDate >= checkOutDate) this.checkOutDate = '';
    },
    emitValues() {
      return {
        checkedInDate: this.checkInDate,
        checkedOutDate: this.checkOutDate,
      };
    },
  },
};
</script>

<style>
.blue--text {
  color: blue;
  margin-bottom: 20px;
}
</style>
