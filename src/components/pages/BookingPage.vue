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
            @change="checkIfShouldClearCheckOutDate"
          ></v-date-picker>
        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import lodash from 'lodash';
export default {
  props: {
    bookingInfo: Object,
  },
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
        const checkOutDate = new Date();
        const currentDay = checkOutDate.getDate();
        checkOutDate.setDate(currentDay + 1);

        return checkOutDate.toISOString().substr(0, 10);
      } else {
        return new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
          .toISOString()
          .substr(0, 10);
      }
    },

    getMinCheckOutDate() {
      const checkOutDate = new Date(this.checkInDate);
      const currentDay = checkOutDate.getDate();
      checkOutDate.setDate(currentDay + 1);
      this.minCheckOutDate = checkOutDate.toISOString().substr(0, 10);

      this.checkIfShouldClearCheckOutDate();
    },

    checkIfShouldClearCheckOutDate() {
      const checkInDate = new Date(this.checkInDate);
      const checkOutDate = new Date(this.checkOutDate);

      if (checkInDate >= checkOutDate) {
        this.checkOutDate = '';
        this.$emit("updateNextButton", true);
      } else {
        const isNextEnabled = checkOutDate.toString() !== 'Invalid Date' && checkInDate.toString() !== 'Invalid Date';
        this.$emit("updateNextButton", !isNextEnabled);
      }
    },

    emitValues() {
      return {
        checkedInDate: this.checkInDate,
        checkedOutDate: this.checkOutDate,
      };
    },

  },
  mounted() {
    const bookingDates = lodash.cloneDeep(this.bookingInfo.bookingDates);
    this.checkInDate = bookingDates.checkedInDate;
    this.checkOutDate = bookingDates.checkedOutDate;

    if(!!this.checkInDate && !!this.checkOutDate) {
      this.getMinCheckOutDate();
    }
  }
};
</script>

<style>
.blue--text {
  color: blue;
  margin-bottom: 20px;
}
</style>
