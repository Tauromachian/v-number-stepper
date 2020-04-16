<template>
  <v-app>
    <number-stepper
      v-model="someNumber"
      show-number
      :min="1"
      :max="3"
      label="Some label"
      :allow-number-editing="false"
    ></number-stepper>
  </v-app>
</template>

<script>
import NumberStepper from "./components/NumberStepper";

export default {
  name: "App",

  components: {
    NumberStepper
  },

  data: () => ({
    someNumber: 1
  })
};
</script>
