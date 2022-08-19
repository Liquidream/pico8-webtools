<template>
  <v-sheet :class="mobile ? undefined : 'pa-12 mx-auto'">
    <v-sheet
      :rounded="mobile ? 'undefined' : 'xl'"
      :elevation="mobile ? undefined : 12"
      color="light-blue-lighten-4"
      class="mx-auto pa-12"
      :width="mobile ? undefined : 800"
    >
      <h1 class="text-h3">PICO-8 Web Tools</h1>
      <span class="text-body-1"
        >This web tool was designed for use with PICO-8 - such as generating QR
        codes for creations made with the online
        <a href="https://www.pico-8-edu.com" target="_blank"
          >Education Edition of PICO-8.</a
        ></span
      >

      <qr-code-generator />
    </v-sheet>
  </v-sheet>
</template>

<script setup lang="ts">
import { useDisplay } from "vuetify";
import QrCodeGenerator from "./QrCodeGenerator.vue";

const { mobile } = useDisplay();
</script>
