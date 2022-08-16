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
          v-model="url"
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

      <v-card width="400" class="mt-5 mx-auto">
        <v-card-item>
          <v-card-title>This is a title</v-card-title>

          <v-card-subtitle>This is a subtitle</v-card-subtitle>
        </v-card-item>

        <v-card-text>This is content</v-card-text>
      </v-card>
    </v-sheet>
  </v-sheet>
</template>

<script setup lang="ts">
  console.log("hello script setup");

  import { ref } from "vue";

  const url = ref("");

  const generateCode = () => {
    console.log("TODO: Generate QR code for " + url.value);
  }
</script>
