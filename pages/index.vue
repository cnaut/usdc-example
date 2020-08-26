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

        <v-row>
          <v-col cols="12" md="6">
            <CVVInput
              v-model="formData.cardData.cvv"
              :rules="[rules.isNumber]"
              default-label="CVV"
              :disabled="loading"
            />
          </v-col>
          <v-col cols="12" md="6">
            <ExpiryInput
              v-model="formData.cardData.expiry"
              :labels="expiryLabels"
              :required="true"
            />
          </v-col>
        </v-row>

        <div class="my-4 subtitle-1 black--text">
          Billing Details
        </div>

        <v-text-field
          v-model="formData.cardData.name"
          :rules="[rules.required]"
          hint="Full name of the card holder"
          label="Cardholder name"
          :disabled="loading"
        />

        <v-text-field
          v-model="formData.cardData.line1"
          :rules="[rules.required]"
          label="Address Line 1"
          :disabled="loading"
        />

        <v-text-field
          v-model="formData.cardData.line2"
          label="Address Line 2"
        />

        <v-text-field
          v-model="formData.cardData.postalCode"
          :rules="[rules.required]"
          label="Postalcode"
          :disabled="loading"
        />

        <v-text-field
          v-model="formData.cardData.city"
          :rules="[rules.required]"
          label="City"
          :disabled="loading"
        />

        <v-text-field
          v-model="formData.cardData.district"
          :rules="[rules.required]"
          label="District"
          :disabled="loading"
          hint="State / County / Province / Region portion of the address. US and Canada use the two-letter code for the subdivision"
        />

    </v-flex>
  </v-layout>
</template>

<script lang="ts">
import AmountInput from '~/components/AmountInput.vue'
import CardInput from '~/components/CardInput.vue'
import CVVInput from '~/components/CVVInput.vue'
import ExpiryInput from '~/components/ExpiryInput.vue'

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
    CardInput,
    CVVInput,
    ExpiryInput
  },
  data: function() {
    return {
      validForm: false,
      loading: false,
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
      },
      rules: {
        isNumber: (v: string) =>
          v === '' || !isNaN(parseInt(v)) || 'Please enter valid number',
        required: (v: string) => !!v || 'Field is required',
      },
      expiryLabels: {
        month: 'Expiry Month',
        year: 'Expiry Year',
      }
    }
  }

}
</script>
