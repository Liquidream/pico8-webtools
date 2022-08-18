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

      <h2 class="text-h4 pt-5">QR-Code Generator</h2>
      <span class="text-body-1"
        >Paste in the URL of your creation (after doing
        <strong>SAVE @URL</strong> in PICO-8) and click to generate.</span
      >
      <v-form ref="form">
        <v-text-field
          v-model="inputUrl"
          class="mt-5"
          label="URL to PICO-8 Content"
          hint="e.g. https://www.pico-8-edu.com/?c=..."
          required
        ></v-text-field>
        <v-btn color="success" class="mr-4" @click="generateCode">
          Generate
        </v-btn>
      </v-form>

      <v-container fill-height fluid>
        <v-row align="center" justify="center">
          <v-col
            class="fill-height d-flex flex-column justify-center align-center"
          >
            <vue-qrcode
              v-if="qrUrl"
              :value="qrUrl"
              @ready="onReady"
            ></vue-qrcode>
          </v-col>
        </v-row>
      </v-container>
    </v-sheet>
  </v-sheet>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useDisplay } from 'vuetify'
import VueQrcode from "@chenfengyuan/vue-qrcode";

const { width, mobile } = useDisplay()

const inputUrl = ref("");
const qrUrl = ref("");

// https://www.pico-8-edu.com/?c=cHJpbnQgImhlbGxvIHdvcmxkIg==&g=w-w-w-w1HQHw-w2Xw-w3Xw-w2HQH
// https://www.pico-8-edu.com/?c=AHB4YQOnAslvcM4NR1zyCNEZ9yfnBssG3-u8wfmXv8GD5E8QPsHxdfMEzUYz9wjtS0RPED1BUjRPUgx02Ss8RLxUh0mXRO8QJHVf9ebo_tQeh4VhJBkw0KSlQkDwDk3cdXU2UUddH1ZRd5loQNg24WVF3YVdVhUv8RDV1kYQln35MEW1MjAzJStyXRBkc5NzV0ZDY0c2E_1bJP3GRLZVPEfU19HcVq5A0D1HNRbOLLaR4EBQBFVW1mvRRPYcC1ExsVadVr3OWwT95sCNR86sFwOj9-Zji8ViccCQkaLm1CZbKRbWxhbK8tbHqG_NXmpl4crX2FzKp-LlwWSjKAy2ZMA9a4x31QHdxPTa6ly8U681Fl8-YfHJBSoJlF2YZqWWQZW2U8oBmRPCJjdNOF64emZvOtsI9vZO2Fp4kvqCPImCvXKmbZ-kiG5DtCDRJwiM4ISVzeTi5JQiq5OoqKrkhqJJkimBgIvfpCkXhk4YXzth7IZo_EW6qd2tcndoaGtAASm64ICBPitP3pkpWkd0verJ2lYdTt1cpPuFDxaSG0YWViYyZZV_ZCFNh8Kl4aSr25V4Jd2YyfIV_YB2Jb0l7tI4uDipiglLmB1lFGbaEAPKLPP6IVmUTbjpBDeMDdjplpU_1yFotybDcGHFBQvJYp62ebsWpGVpTStEkS9Xi6E4Wu2SQT8tJGGattFKFJmqLKdm91YXhs7eaDcMc8UBVxZzK8XIxAlpFA_KkQiSDuxNjYTzW1IKQevEpJUnaY8o083JbKurTnBBvam5UldTWT6wVi9Eg9FisDubqgQIR9TxYFn3C3NKAhtVqRdUZyYoFU2a0jeRokkUZhN7kgwLqR7SRjUzY4u9uQd4i_NfYC56h_E3OP8ZmofIym4rf4ZckWJupbpgZGZuZ0uYonyBdxh4icdInuEtHmJpKa0nr0g2r9hLRlakTAA=&g=w-w-w-w1HQHw-w2Xw-w3Xw-w2HQH

const generateCode = () => {
  console.log("TODO: Generate QR code for " + inputUrl.value);
  qrUrl.value = inputUrl.value;
};

const onReady = (canvas: any) => {
  const context = canvas.getContext("2d");
  const image = new Image();
  // https://vitejs.dev/guide/build.html#public-base-path
  image.src = import.meta.env.BASE_URL + "lexaloffle-pico8.png";
  image.crossOrigin = "anonymous";
  image.onload = () => {
    const coverage = 0.15;
    const width = Math.round(canvas.width * coverage);
    const x = (canvas.width - width) / 2;

    context.drawImage(image, x, x, width, width);
  };
};
</script>
