<template>
  <v-container fluid>
    <v-layout justify-center align-center>
      <v-flex xs12>
        <div class="budget-box">
          <h1 class="blue--text text-center">Budget</h1>
          <v-layout justify-center>
            <v-btn class="mb-3" color="primary">
              <v-icon style="color: transparent">mdi-currency-usd</v-icon>
              <v-icon>mdi-currency-usd</v-icon>
              <v-icon style="color: transparent">mdi-currency-usd</v-icon>
            </v-btn>
            <v-btn class="mb-3 ml-10" color="primary">
              <v-icon>mdi-currency-usd</v-icon>
              <v-icon style="color: transparent">mdi-currency-usd</v-icon>
              <v-icon>mdi-currency-usd</v-icon>
            </v-btn>
            <v-btn class="ml-10" color="primary">
              <v-icon>mdi-currency-usd</v-icon>
              <v-icon>mdi-currency-usd</v-icon>
              <v-icon>mdi-currency-usd</v-icon>
            </v-btn>
          </v-layout>
        </div>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  methods: {
    setBudgetType(budgetTypeIndex) {
      this.index = budgetTypeIndex;
    },

    emitValues() {
      return this.budgetType[this.index];
    },
  },
};
</script>

<style>
.blue--text {
  color: blue;
  margin-bottom: 20px;
}
.text-center {
  text-align: center;
}
.budget-box {
  width: 650px;
  padding: 20px;
  margin: 0 auto;
  text-align: center;
}
.mb-3 {
  margin-bottom: 30px;
}

.invisibile-icons {
  color: transparent;
}
</style>
