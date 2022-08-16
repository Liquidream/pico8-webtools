<template>
  <v-sheet class="pa-12 mx-auto">
    <v-sheet
      rounded="xl"
      elevation="12"
      color="light-blue-lighten-3"
      class="mx-auto pa-12"
      width="800"
    >
      <h1 class="text-h3">PICO-8 Web Tools</h1>
      <span class="text-body-1">sdsdsdsfsdf</span>

      <h2 class="text-h4 pt-5">QR-Code Generator</h2>
      <span class="text-body-1">sdsdsdsfsdf</span>
      <v-form ref="form">
        <v-text-field
          v-model="inputUrl"
          label="URL to PICO-8 Content"
          hint="e.g. 'https://www.pico-8-edu.com/?c=...''"
          required
        ></v-text-field>
        <v-btn
          color="success"
          class="mr-4"
          @click="generateCode"
        >
          Generate
        </v-btn>
      </v-form>

      <!-- <v-card width="400" class="mt-5 mx-auto">
        <v-card-item>
          <v-card-title>This is a title</v-card-title>

          <v-card-subtitle>This is a subtitle</v-card-subtitle>
        </v-card-item>

        <v-card-text>This is content</v-card-text>
      </v-card> --> 
      <div class="mt-5 mx-auto" width="200px">
        <vue-qrcode :value="qrUrl" ></vue-qrcode>
      </div>
    </v-sheet>
  </v-sheet>
</template>

<script setup lang="ts">  
  console.log("hello script setup");

  import { ref } from "vue";
  import VueQrcode from '@chenfengyuan/vue-qrcode';

  const inputUrl = ref("");
  const qrUrl = ref("");

  // https://www.pico-8-edu.com/?c=cHJpbnQgImhlbGxvIHdvcmxkIg==&g=w-w-w-w1HQHw-w2Xw-w3Xw-w2HQH
  // https://www.pico-8-edu.com/?c=AHB4YQOnAslvcM4NR1zyCNEZ9yfnBssG3-u8wfmXv8GD5E8QPsHxdfMEzUYz9wjtS0RPED1BUjRPUgx02Ss8RLxUh0mXRO8QJHVf9ebo_tQeh4VhJBkw0KSlQkDwDk3cdXU2UUddH1ZRd5loQNg24WVF3YVdVhUv8RDV1kYQln35MEW1MjAzJStyXRBkc5NzV0ZDY0c2E_1bJP3GRLZVPEfU19HcVq5A0D1HNRbOLLaR4EBQBFVW1mvRRPYcC1ExsVadVr3OWwT95sCNR86sFwOj9-Zji8ViccCQkaLm1CZbKRbWxhbK8tbHqG_NXmpl4crX2FzKp-LlwWSjKAy2ZMA9a4x31QHdxPTa6ly8U681Fl8-YfHJBSoJlF2YZqWWQZW2U8oBmRPCJjdNOF64emZvOtsI9vZO2Fp4kvqCPImCvXKmbZ-kiG5DtCDRJwiM4ISVzeTi5JQiq5OoqKrkhqJJkimBgIvfpCkXhk4YXzth7IZo_EW6qd2tcndoaGtAASm64ICBPitP3pkpWkd0verJ2lYdTt1cpPuFDxaSG0YWViYyZZV_ZCFNh8Kl4aSr25V4Jd2YyfIV_YB2Jb0l7tI4uDipiglLmB1lFGbaEAPKLPP6IVmUTbjpBDeMDdjplpU_1yFotybDcGHFBQvJYp62ebsWpGVpTStEkS9Xi6E4Wu2SQT8tJGGattFKFJmqLKdm91YXhs7eaDcMc8UBVxZzK8XIxAlpFA_KkQiSDuxNjYTzW1IKQevEpJUnaY8o083JbKurTnBBvam5UldTWT6wVi9Eg9FisDubqgQIR9TxYFn3C3NKAhtVqRdUZyYoFU2a0jeRokkUZhN7kgwLqR7SRjUzY4u9uQd4i_NfYC56h_E3OP8ZmofIym4rf4ZckWJupbpgZGZuZ0uYonyBdxh4icdInuEtHmJpKa0nr0g2r9hLRlakTAA=&g=w-w-w-w1HQHw-w2Xw-w3Xw-w2HQH

  const generateCode = () => {
    console.log("TODO: Generate QR code for " + inputUrl.value);
    qrUrl.value = inputUrl.value
  }
</script>
