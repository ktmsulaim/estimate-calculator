<template>
  <v-row justify="center">
    <v-col cols="6" md="6">
      <v-card>
        <v-card-title>Price Calculator</v-card-title>
        <v-card-text>
          <v-row>
            <v-col cols="6">
              <v-select
                :items="currencyList"
                label="Currency"
                item-text="text"
                item-value="value"
                v-model="currency"
                @change="updateExchangeRate"
              ></v-select>
            </v-col>
            <v-col cols="6">
              <v-text-field
                label="Exchange Rate"
                v-model="exchangeRate"
                :disabled="currency.value === 'inr'"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="6">
              <v-text-field label="Amount" type="number" v-model="amount"></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-text-field label="GST" v-model="percentage"></v-text-field>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
      <v-card class="mt-2">
        <v-list-item three-line>
          <v-list-item-content>
            <v-list-item-subtitle>
              GST: {{ format(gst) }}
            </v-list-item-subtitle>
            <v-list-item-subtitle>
              Sub Total: {{ format(subTotal) }}
            </v-list-item-subtitle>
            <v-list-item-title>Total: {{ format(total) }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      amount: 0,
      percentage: 18,
      currency: { text: "USD", value: "usd" },
      exchangeRate: 74.38,
    };
  },
  computed: {
    currencyList() {
      return [
        {
          text: "INR",
          value: "inr",
        },
        {
          text: "USD",
          value: "usd",
        },
      ];
    },
    parsedAmount() {
        return this.amount ? parseFloat(this.amount) : 0;
    },
    gst() {
      if (this.parsedAmount > 0) {
        let gstAmount = (this.parsedAmount * 18) / 100;

        if(this.currency.value === 'usd') {
            return gstAmount * this.exchangeRate;
        } else {
            return gstAmount;
        }
      }

      return 0;
    },
    subTotal() {
      if (this.currency.value === "usd") {
        return this.parsedAmount * this.exchangeRate;
      } else {
        return this.parsedAmount;
      }
    },
    total() {
      if (this.parsedAmount > 0) {
          return this.subTotal + this.gst;
      } else {
        return 0;
      }
    },
  },
  methods: {
      format(amount) {
          return Intl.NumberFormat('en-IN', {style: 'currency', currency: 'INR'}).format(amount)
      },
  }
};
</script>

<style>
</style>