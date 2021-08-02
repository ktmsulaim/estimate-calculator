<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
     <v-app-bar-title>KTM</v-app-bar-title>

    </v-app-bar>

    <v-main>
      <v-container>
        <PriceCalculator/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import PriceCalculator from './components/PriceCalculator';

export default {
  name: 'App',

  components: {
    PriceCalculator,
  },

  data: () => ({
    //
  }),
};
</script>
