<template>
  <v-sheet :class="mobile ? undefined : 'pt-12 pl-12 pr-12 pb-6 mx-auto'">
    <v-sheet
      :rounded="mobile ? 'undefined' : 'xl'"
      :elevation="mobile ? undefined : 12"
      color="light-blue-lighten-4"
      class="mx-auto pa-12"
      :width="mobile ? undefined : 800"
    >
      <!-- <v-img src="lexaloffle-pico8.png" height="64px"></v-img> -->
      <div class="header">
        <img :src="pico8icon" />
        <h1 class="text-h3">PICO-8 Web Tools</h1>
      </div>
      <div class="text-body-1 pt-5" style="clear: both">
        These web tools are designed for use with the
        <a href="https://www.pico-8-edu.com" target="_blank"
          >Education Edition of PICO-8.</a
        ><br />Such as generating QR codes or Itch.io web files for your
        creations.
      </div>
      <qr-code-generator />
      <itch-zip-builder />
    </v-sheet>
  </v-sheet>
  <my-footer />
</template>

<script setup lang="ts">
import { useDisplay } from "vuetify";
import QrCodeGenerator from "./QrCodeGenerator.vue";
import ItchZipBuilder from "./ItchZipBuilder.vue";
import MyFooter from "./MyFooter.vue";

const { mobile } = useDisplay();
const pico8icon = import.meta.env.BASE_URL + "lexaloffle-pico8.png";
</script>

<style>
.header img {
  float: left;
  width: 50px;
}

.header h1 {
  position: relative;
  left: 10px;
}

a:link, a:visited {
    color: #2962FF;
}

/* Add a slight gap at bottom of hint text */
.v-messages {
  margin-bottom: 5px;
}
</style>
