<template>
  <div class="destination-page">
    <h1 class="blue--text">Choose Destination</h1>
      <div class="input-container">
        <div class="container">
        <v-icon class="map-icon">mdi-map-marker</v-icon>
        <v-text-field
            v-model="address"
            :rules="addressRules"
            label="Enter address"
            required
            @keydown.enter="getCoordinates"
            @input="checkTheAddressLength"
          ></v-text-field>
        </div>
      </div>
      <button @click="getCoordinates" class="blue--text"><h3>Confirm</h3></button>
      <p v-if="statusMessage.length > 0" :class="{ 
        'success--text': this.statusMessage === requestStatusMessages[0], 
        'warning--text': this.statusMessage === requestStatusMessages[1], 
        'error--text': this.statusMessage === requestStatusMessages[2]}"> 
        {{ statusMessage }}
      </p>
  </div>
</template>

<script>
import axios from 'axios';
import lodash from 'lodash';
export default {
  props: {
    bookingInfo: Object,
  },
  data() {
    return {
      address: '',
      currentAddress: '',
      statusMessage: '',
      latitude: null,
      longitude: null,
      requestStatusMessages: [
        'Your destination is added successfully!',
        'Address cannot be found!',
        'You must enter an address!'
      ],
      addressRules: [
      (v) => !!v || 'Address is required',
      (v) =>
        (v && v.trim().length > 3) || 'Address must contain more than 3 characters',
      ],
    };
  },
  methods: {
    async getCoordinates() {
      if(this.address.trim().length > 3) {
          try {
          const apiKey = '9bebfc7f44844ab09b471229dc788e32';
          const response = await axios.get(
            'https://api.opencagedata.com/geocode/v1/json',
            {
              params: {
                key: apiKey,
                q: this.address,
              },
            }
          );

          const location = response.data.results[0].geometry;
          
          this.setCoordinates(location.lat, location.lng, this.address);
          this.statusMessage = this.requestStatusMessages[0];
          this.$emit("updateNextButton", false);

        } catch (error) {
          this.setCoordinates(null, null, null);
          this.statusMessage = this.requestStatusMessages[1];
          this.$emit("updateNextButton", true);
        }
      } else {
        this.setCoordinates(null, null, null);
        this.statusMessage = this.requestStatusMessages[2];
        this.$emit("updateNextButton", true);
      }
    },

    setCoordinates(latitude, longitude, currentAddress) {
      this.latitude = latitude;
      this.longitude = longitude;
      this.currentAddress = currentAddress;
    },

    emitValues() {
      return {
        latitude: this.latitude,
        longitude: this.longitude,
        address: this.address,
      };
    },

    checkTheAddressLength() {
      const isNextEnabled = this.address === this.currentAddress;
      this.$emit("updateNextButton", !isNextEnabled);
    }
  },
  mounted() {
    const destinationCoordinates = lodash.cloneDeep(this.bookingInfo.destinationCoordinates);
    this.address = destinationCoordinates.address;
    this.currentAddress = destinationCoordinates.address;
    this.latitude = destinationCoordinates.latitude;
    this.longitude = destinationCoordinates.longitude;

    const isNextEnabled = this.address.length > 3 && !!this.latitude && !!this.longitude && this.address === this.currentAddress;
    this.$emit("updateNextButton", !isNextEnabled);
  }
};
</script>

<style scoped>
.destination-page {
  text-align: center;
  padding-top: 40px;
}

.blue--text {
  color: blue;
  margin-bottom: 20px;
}

.warning--text {
  color: orange;
}

.success--text {
  color: lime;
}

.error--text {
  color: red;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  width: 400px;
}

.input-container {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
 
}

.map-icon {
  color: blue;
  margin-right: 10px;
}
</style>
