<template>
  <div class="destination-page">
    <h1 class="blue--text">Choose Destination</h1>
    <div class="input-container">
      <v-icon class="map-icon">mdi-map-marker</v-icon>
      <input v-model="address" placeholder="Enter address" />
    </div>
    <button @click="getCoordinates" class="blue--text"><h3>Confirm</h3></button>
    <p class="green--text" v-if="latitude && longitude">
      We have the correct address please continue
    </p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      address: '',
      latitude: null,
      longitude: null,
    };
  },
  methods: {
    async getCoordinates() {
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
        this.latitude = location.lat;
        this.longitude = location.lng;

        console.log(location, this.latitude, this.longitude);
      } catch (error) {
        console.error('Error getting coordinates:', error);
      }
    },
  },
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
