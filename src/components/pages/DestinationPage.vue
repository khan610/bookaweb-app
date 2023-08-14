<template>
  <div>
    <h1 class="blue--text">Unesite Adresu</h1>
    <vue-google-autocomplete
      v-if="googleLoaded"
      v-model="address"
      id="autocomplete"
      classname="form-control"
      placeholder="Unesite adresu i broj"
      :options="options"
      :api-key="googleMapsApiKey"
      @placechanged="onPlaceChanged"
    ></vue-google-autocomplete>
  </div>
</template>

<script>
import VueGoogleAutocomplete from 'vue-google-autocomplete';

export default {
  components: {
    VueGoogleAutocomplete,
  },
  data() {
    return {
      googleLoaded: false,
      address: '',
      options: {
        types: ['geocode'],
      },
      googleMapsApiKey: 'AIzaSyCLGp44kYkaz2PHvU4RC2LM62kRbaRN7JA',
    };
  },
  methods: {
    onPlaceChanged(place) {
      if (window.google) {
        console.log(place);
      } else {
        console.error('Google Maps API nije učitan.');
      }
    },
  },
  mounted() {
    const googleScript = document.createElement('script');
    googleScript.src = `https://maps.googleapis.com/maps/api/js?key=${this.googleMapsApiKey}&libraries=places`;
    googleScript.onload = () => {
      this.googleLoaded = true;
    };
    document.head.appendChild(googleScript);
  },
};
</script>

<style>
.blue--text {
  color: blue;
  margin-bottom: 20px;
}
</style>
