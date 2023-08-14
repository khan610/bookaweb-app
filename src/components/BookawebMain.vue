<template>
  <div>
    <info-page></info-page>
    <!-- <v-btn class="ma-2" color="orange-darken-2">
      <v-icon>mdi-arrow-left</v-icon>
      Back
    </v-btn>
    <v-btn class="ma-2" color="primary">
      Next
      <v-icon>mdi-checkbox-marked-circle</v-icon>
    </v-btn> -->
  </div>
</template>

<script>
export default {
  components: {
    // 'destination-page': require('@/components/pages/DestinationPage.vue')
    //   .default,
    // 'services-page': require('@/components/pages/ServicesPage.vue').default,
    // 'booking-page': require('@/components/pages/BookingPage.vue').default,
    // 'budget-page': require('@/components/pages/BudgetPage.vue').default,
    'info-page': require('@/components/pages/InfoPage.vue').default,
  },
};
</script>

<style></style>

<!-- <destination-page></destination-page>
    <services-page></services-page>
    <booking-page></booking-page>
    <budget-page></budget-page>
    <info-page></info-page> -->
