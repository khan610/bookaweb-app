<template>
  <div class="container">
    <div class="icon-wraper">
      <div class="icon-button icon-button-1">
        <v-btn icon color="primary">
          <v-icon>mdi-currency-usd</v-icon>
        </v-btn>
      </div>
      <div class="icon-button icon-button-2">
        <v-btn icon color="primary">
          <v-icon>mdi-currency-usd</v-icon>
          <v-icon>mdi-currency-usd</v-icon>
        </v-btn>
      </div>
      <div class="icon-button icon-button-3">
        <v-btn icon color="primary">
          <v-icon>mdi-currency-usd</v-icon>
          <v-icon>mdi-currency-usd</v-icon>
          <v-icon>mdi-currency-usd</v-icon>
        </v-btn>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.icon-wraper {
  display: flex;
  position: relative;
  width: 50%;
  justify-content: space-evenly;
  background-color: blue;
}
</style>
