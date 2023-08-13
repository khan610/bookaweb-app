<template>
  <div>
    <destination-page></destination-page>
    <!-- <services-page></services-page> -->
    <booking-page></booking-page>
    <budget-page></budget-page>
    <info-page></info-page>
  </div>
</template>

<script>
export default {
  components: {
    'destination-page': require('@/components/pages/DestinationPage.vue')
      .default,
    // 'services-page': require('@/components/pages/ServicesPage.vue').default,
    'booking-page': require('@/components/pages/BookingPage.vue').default,
    'budget-page': require('@/components/pages/BudgetPage.vue').default,
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
