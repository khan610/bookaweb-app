<template>
  <div class="flex">
    <div class="date-picker-div">
      <h1>Check-In</h1>
      <v-row justify="center" class="row">
        <v-date-picker
          v-model="checkInDate"
          color="primary"
          :min="minCheckInDate"
          @change="getMinCheckOutDate"
        ></v-date-picker>
      </v-row>
    </div>
    <div class="date-picker-div">
      <h1>Check-Out</h1>
      <v-row justify="center" class="row">
        <v-date-picker
          v-model="checkOutDate"
          color="primary"
          :min="minCheckOutDate"
        ></v-date-picker>
      </v-row>
    </div>
  </div>
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
  },
};
</script>

<style>
.flex {
  display: flex;
  justify-content: center;
  align-items: center;
}

.row {
  margin: 0 !important;
}

.date-picker-div {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  width: 35%;
}
</style>
