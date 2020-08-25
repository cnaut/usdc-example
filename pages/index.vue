<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
        <AmountInput
          v-model="formData.amount"
          label="Amount"
          :disabled="loading"
        />

        
        <CardInput
          v-model="formData.cardData.cardNumber"
          label="Card Number"
          :disabled="loading"
        />
    </v-flex>
  </v-layout>
</template>

<script lang="ts">
import AmountInput from '~/components/AmountInput.vue'
import CardInput from '~/components/CardInput.vue'

interface FormData {
  amount: string
  cardData: {
    cardNumber: string
    cvv: string
    expiry: {
      month: string
      year: string
    }
    name: string
    country: string
    district: string
    line1: string
    line2: string
    city: string
    postalCode: string
    phoneNumber: string
    email: string
  }
}

export default {
  components: {
    AmountInput,
    CardInput
  },
  data: function() {
    return {
      validForm: false,
      formData: {
        amount: '0.00',
        cardData: {
          cardNumber: '',
          cvv: '',
          expiry: {
            month: '',
            year: '',
          },
          name: '',
          country: '',
          district: '',
          line1: '',
          line2: '',
          city: '',
          postalCode: '',
          phoneNumber: '',
          email: '',
        },
      }
    }
  }

}
</script>
