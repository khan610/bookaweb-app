<template>
  <v-app>
    <v-app-bar app color="primary" fixed>
      <v-container>
        <v-layout align-center>
          <v-icon color="white">mdi-book</v-icon>
          <h1 class="white--text ml-2 mr-4">Bookaweb</h1>
          <v-spacer></v-spacer>
        </v-layout>
      </v-container>
    </v-app-bar>
    <v-main>
      <destination-page></destination-page>
      <services-page></services-page>
      <booking-page></booking-page>
      <budget-page></budget-page>
      <info-page></info-page>
    </v-main>
  </v-app>
</template>
<script>
export default {
  components: {
    'destination-page': require('@/components/pages/DestinationPage.vue')
      .default,
    'services-page': require('@/components/pages/ServicesPage.vue').default,
    'booking-page': require('@/components/pages/BookingPage.vue').default,
    'budget-page': require('@/components/pages/BudgetPage.vue').default,
    'info-page': require('@/components/pages/InfoPage.vue').default,
  },
};
</script>

<style></style>
