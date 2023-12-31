<template>
  <div>
    <v-layout align-center justify-center column>
      <h1 class="blue--text text-center">Your Info</h1>
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-text-field
          v-model="firstName"
          :rules="firstNameRules"
          label="First name"
          required
          @input="setNextButton"
        ></v-text-field>

        <v-text-field
          v-model="lastName"
          :rules="lastNameRules"
          label="Last name"
          required
          @input="setNextButton"
        ></v-text-field>

        <v-text-field
          v-model="email"
          :rules="emailRules"
          label="E-mail"
          required
          @input="setNextButton"
        ></v-text-field>

        <v-text-field
          v-model="phone"
          :rules="phoneRules"
          label="Phone Number"
          required
          maxlength="10"
          @keydown="numbersOnly"
          @input="setNextButton"
        ></v-text-field>
      </v-form>
    </v-layout>
  </div>
</template>

<script>
import lodash from 'lodash';
export default {
  props: {
    bookingInfo: Object,
  },
  data: () => ({
    valid: true,
    firstName: '',
    firstNameRules: [
      (v) => !!v || 'First name is required',
      (v) =>
        (v && v.length <= 10) || 'First name must be less than 10 characters',
    ],
    lastName: '',
    lastNameRules: [
      (v) => !!v || 'Last name is required',
      (v) =>
        (v && v.length <= 10) || 'Last name must be less than 10 characters',
    ],
    email: '',
    emailRules: [
      (v) => !!v || 'E-mail is required',
      (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    phone: '',
    phoneRules: [
      (v) => !!v || 'Phone is required',
      (v) =>
        /^(011|060|061|062|063|064|065|066)\d{7}$/.test(v) ||
        'Phone must start with 011, 060, 061, 062, 063, 064, 065, or 066 and have 10 digits',
      (v) =>
        (v && v.length <= 10) ||
        'Phone must be less than or equal to 10 digits',
    ],
  }),
  methods: {
    validate() {
      return this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
    emitValues() {
      return {
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
        phoneNumber: this.phone,
      };
    },
    numbersOnly() {
      const charCode = event.which ? event.which : event.keyCode;
      const isNumericKey =
        (charCode >= 48 && charCode <= 57) ||
        (charCode >= 96 && charCode <= 105);

      if (
        !isNumericKey &&
        charCode !== 46 &&
        charCode !== 8 &&
        charCode !== 37 &&
        charCode !== 39
      ) {
        event.preventDefault();
      }
    },
    setNextButton() {
      if (
        this.firstName.length > 0 &&
        this.lastName.length > 0 &&
        this.email.length > 0 &&
        this.phone.length > 0
      ) {
        const isNextEnabled = this.$refs.form.validate();
        this.$emit('updateNextButton', !isNextEnabled);
      } else {
        this.$emit('updateNextButton', true);
      }
    },
  },

  mounted() {
    const personalInfo = lodash.cloneDeep(this.bookingInfo.personalInfo);
    this.firstName = personalInfo.firstName;
    this.lastName = personalInfo.lastName;
    this.email = personalInfo.email;
    this.phone = personalInfo.phoneNumber;
    this.setNextButton();
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
</style>
