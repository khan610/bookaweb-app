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
      <component :is="currentComponent" ref="pageRef" :bookingInfo="booking" @updateNextButton="updateNextButton"></component>
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
              @click="showNextComponent"
              color="primary"
              class="float-right"
              :label="forwardBtnLabel"
              :disabled="isNextDisabled"
            >
              {{ forwardBtnLabel }}
            </v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>
import lodash from 'lodash';
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
      isNextDisabled: true,
      currentComponent: 'destination-page',
      components: [
        'destination-page',
        'services-page',
        'booking-page',
        'budget-page',
        'info-page',
      ],
      booking: {
        budgetType: '',
        selectedServices: [],
        destinationCoordinates: {
          latitude: null,
          longitude: null,
          address: '',
        },
        bookingDates: {
          checkedInDate: '',
          checkedOutDate: '',
        },
        personalInfo: {
          firstName: '',
          lastName: '',
          email: '',
          phoneNumber: '',
        },
      },
    };
  },
  methods: {
    showNextComponent() {
      this.updateBookingObject();
      
      if(this.currentComponent === 'info-page') {
        const bookingComplete = lodash.cloneDeep(this.booking);
        console.log(bookingComplete);
      }
      
      const currentIndex = this.components.indexOf(this.currentComponent);
      if (currentIndex < this.components.length - 1) {
        this.currentComponent = this.components[currentIndex + 1];
        this.isNextDisabled = true;
      }
    },
    showPreviousComponent() {
      this.updateBookingObject();

      const currentIndex = this.components.indexOf(this.currentComponent);
      if (currentIndex > 0) {
        this.currentComponent = this.components[currentIndex - 1];
        this.isNextDisabled = false;
      }
    },
    assignEmittedValue(value) {
      switch (this.currentComponent) {
        case 'destination-page': {
          this.booking.destinationCoordinates = { ...value };
          break;
        }
        case 'services-page': {
          this.booking.selectedServices = value;
          break;
        }
        case 'booking-page': {
          this.booking.bookingDates = { ...value };
          break;
        }
        case 'budget-page': {
          this.booking.budgetType = value;
          break;
        }
        case 'info-page': {
          this.booking.personalInfo = { ...value };
          break;
        }
        default:
          break;
      }
    },
    updateBookingObject() {
      const emittedValue = this.$refs.pageRef.emitValues();
      this.assignEmittedValue(emittedValue);
    },
    updateNextButton(value) {
      this.isNextDisabled = value;
    }
  },

  computed: {
    forwardBtnLabel() {
      return this.currentComponent === 'info-page' ? 'Done' : 'Next';
    },
  },
};
</script>

<style>
.v-application {
  padding-top: 40px;
}
</style>
