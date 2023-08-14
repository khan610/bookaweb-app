<template>
  <div>
    <div>
      <budget-page></budget-page>

      <div>
        <v-btn color="orange-darken-2">
          <v-icon>mdi-arrow-left</v-icon>
          Back
        </v-btn>
        <v-btn color="primary">
          Next
          <v-icon>mdi-checkbox-marked-circle</v-icon>
        </v-btn>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {
    // 'destination-page': require('@/components/pages/DestinationPage.vue')
    //   .default,
    // 'services-page': require('@/components/pages/ServicesPage.vue').default,
    //'booking-page': require('@/components/pages/BookingPage.vue').default,
    'budget-page': require('@/components/pages/BudgetPage.vue').default,
    // 'info-page': require('@/components/pages/InfoPage.vue').default,
    //'bookaweb-top': require('@/components/BookawebTop.vue').default,
  },
};
</script>

<style>
</style>

<!-- <destination-page></destination-page>
    <services-page></services-page>
    <booking-page></booking-page>
    <budget-page></budget-page>
    <info-page></info-page> -->
