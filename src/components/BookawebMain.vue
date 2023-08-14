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
      <component :is="currentComponent"></component>
    </v-main>
    <v-footer app>
      <v-container>
        <v-layout>
          <v-flex xs6>
            <v-btn
              v-if="currentComponent !== 'destination-page'"
              @click="showPreviousComponent"
              color="primary"
            >
              Back
            </v-btn>
          </v-flex>
          <v-flex xs6>
            <v-btn
              v-if="currentComponent !== 'info-page'"
              @click="showNextComponent"
              color="primary"
              class="float-right"
            >
              Next
            </v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-footer>
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
  data() {
    return {
      currentComponent: 'destination-page',
      components: [
        'destination-page',
        'services-page',
        'booking-page',
        'budget-page',
        'info-page',
      ],
    };
  },
  methods: {
    showNextComponent() {
      const currentIndex = this.components.indexOf(this.currentComponent);
      if (currentIndex < this.components.length - 1) {
        this.currentComponent = this.components[currentIndex + 1];
      }
    },
    showPreviousComponent() {
      const currentIndex = this.components.indexOf(this.currentComponent);
      if (currentIndex > 0) {
        this.currentComponent = this.components[currentIndex - 1];
      }
    },
  },
};
</script>

<style></style>
