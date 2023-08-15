<template>
  <div>
    <h1>OpenCage API Example</h1>
    <input v-model="address" placeholder="Enter address" />
    <button @click="getCoordinates">Get Coordinates</button>
    <p v-if="latitude && longitude">
      Latitude: {{ latitude }}<br />
      Longitude: {{ longitude }}
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
