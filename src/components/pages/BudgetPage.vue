<template>
  <v-container fluid>
    <v-layout justify-center align-center>
      <v-flex xs12>
        <div class="budget-box">
          <h1 class="blue--text text-center">Budget</h1>
          <v-layout justify-center>
            <v-btn
              class="mb-3"
              color="primary"
              @click="setBudgetType(0)"
              :outlined="index !== 0"
            >
              <v-icon style="color: transparent">mdi-currency-usd</v-icon>
              <v-icon>mdi-currency-usd</v-icon>
              <v-icon style="color: transparent">mdi-currency-usd</v-icon>
            </v-btn>
            <v-btn
              class="mb-3 ml-10"
              color="primary"
              @click="setBudgetType(1)"
              :outlined="index !== 1"
            >
              <v-icon>mdi-currency-usd</v-icon>
              <v-icon style="color: transparent">mdi-currency-usd</v-icon>
              <v-icon>mdi-currency-usd</v-icon>
            </v-btn>
            <v-btn
              class="ml-10"
              color="primary"
              @click="setBudgetType(2)"
              :outlined="index !== 2"
            >
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
  props: {
    bookingInfo: Object,
  },
  data() {
    return {
      budgetType: ['Standard', 'Premium', 'Deluxe'],
      index: 3,
      selectedBudgetType: '',
    };
  },
  methods: {
    setBudgetType(budgetTypeIndex) {
      this.index = budgetTypeIndex;
      this.selectedBudgetType = this.budgetType[this.index];
      this.setNextButton();
    },

    emitValues() {
      return this.selectedBudgetType;
    },

    setNextButton() {
      const isNextEnabled = this.selectedBudgetType.length > 0 && this.index < 3 ;
      this.$emit("updateNextButton", !isNextEnabled);
    }
  },
  mounted() {
    const budgetType = this.bookingInfo.budgetType;
    this.selectedBudgetType = budgetType;
    this.index = this.budgetType.indexOf(budgetType);

    this.setNextButton();
  }
};
</script>

<style scoped>
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
</style>
