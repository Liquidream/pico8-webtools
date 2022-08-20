<template>
  <h2 class="text-h4 pt-5">Itch.io HTML File Builder</h2>
  <span class="text-body-1"
    >Paste in the URL of your creation (after doing
    <strong>SAVE @URL</strong> in PICO-8) and click to download a HTML file,
    which you can upload to a 
    <a href="https://itch.io/game/new/" target="_blank">new Itch.io project</a>
    (e.g. to submit a jam entry).</span
  >
  <v-form ref="form">
    <v-text-field
      v-model="inputUrl"
      class="mt-5"
      label="URL to PICO-8 Content"
      hint="e.g. https://www.pico-8-edu.com/?c=..."
      required
    ></v-text-field>
    <v-btn
      :disabled="!inputUrl"
      color="success"
      class="mr-4"
      @click="downloadHtml"
    >
      Download
    </v-btn>
  </v-form>
</template>

<script setup lang="ts">
import { ref } from "vue";
import FileSaver from "file-saver";
//import JSZip from "jszip";

const inputUrl = ref("");

const templateContent =
  '<!DOCTYPE html>\n<html>\n  <body style="margin: 0; padding: 0; height: 100%; width: 100%; background-color:#111111">\n    <!-- \n	  Src value below should be your URL from PICO-8 Education Edition \n	  (after doing: SAVE @URL from PICO-8 console) \n	-->\n    <iframe style="height: 555px; width: 100%;" scrolling="no" frameborder="0" \n		src="[[URL]]">\n	</iframe>\n  </body>\n</html>';

// const templateContent =
//   "<&lt;!DOCTYPE html&gt;\n&lt;html&gt;\n  &lt;body style=&quot;margin: 0; padding: 0; height: 100%; width: 100%; background-color:#111111&quot;&gt;\n    &lt;!-- \n	  Replace src value below with URL from PICO-8 Education Edition \n	  (after doing: SAVE @URL from PICO-8 console) \n	--&gt;\n    &lt;iframe style=&quot;height: 555px; width: 100%;&quot; scrolling=&quot;no&quot; frameborder=&quot;0&quot; \n		src=&quot;https://www.pico-8-edu.com/?c=OjpfOjoKcHJpbnQoIocgaXRjaC5pbyBydWxlcyCHIixybmQoMTUpKQpmbGlwKCkKZ290byBf&amp;g=w-w-w-w1HQHw-w2Xw-w3Xw-w2HQH&quot;&gt;\n	&lt;/iframe&gt;\n  &lt;/body&gt;\n&lt;/html&gt;";
//const templateContent = "&lt;!DOCTYPE html&gt; &lt;html&gt; &lt;body style=&quot;margin: 0; padding: 0; height: 100%; width: 100%; background-color:#111111&quot;&gt; &lt;!-- Replace src value below with URL from PICO-8 Education Edition (after doing: SAVE @URL from PICO-8 console) --&gt; &lt;iframe style=&quot;height: 555px; width: 100%;&quot; scrolling=&quot;no&quot; frameborder=&quot;0&quot; src=&quot;https://www.pico-8-edu.com/?c=OjpfOjoKcHJpbnQoIocgaXRjaC5pbyBydWxlcyCHIixybmQoMTUpKQpmbGlwKCkKZ290byBf&amp;g=w-w-w-w1HQHw-w2Xw-w3Xw-w2HQH&quot;&gt; &lt;/iframe&gt; &lt;/body&gt; &lt;/html&gt;"\n"

// https://www.pico-8-edu.com/?c=cHJpbnQgImhlbGxvIHdvcmxkIg==&g=w-w-w-w1HQHw-w2Xw-w3Xw-w2HQH
// https://www.pico-8-edu.com/?c=AHB4YQOnAslvcM4NR1zyCNEZ9yfnBssG3-u8wfmXv8GD5E8QPsHxdfMEzUYz9wjtS0RPED1BUjRPUgx02Ss8RLxUh0mXRO8QJHVf9ebo_tQeh4VhJBkw0KSlQkDwDk3cdXU2UUddH1ZRd5loQNg24WVF3YVdVhUv8RDV1kYQln35MEW1MjAzJStyXRBkc5NzV0ZDY0c2E_1bJP3GRLZVPEfU19HcVq5A0D1HNRbOLLaR4EBQBFVW1mvRRPYcC1ExsVadVr3OWwT95sCNR86sFwOj9-Zji8ViccCQkaLm1CZbKRbWxhbK8tbHqG_NXmpl4crX2FzKp-LlwWSjKAy2ZMA9a4x31QHdxPTa6ly8U681Fl8-YfHJBSoJlF2YZqWWQZW2U8oBmRPCJjdNOF64emZvOtsI9vZO2Fp4kvqCPImCvXKmbZ-kiG5DtCDRJwiM4ISVzeTi5JQiq5OoqKrkhqJJkimBgIvfpCkXhk4YXzth7IZo_EW6qd2tcndoaGtAASm64ICBPitP3pkpWkd0verJ2lYdTt1cpPuFDxaSG0YWViYyZZV_ZCFNh8Kl4aSr25V4Jd2YyfIV_YB2Jb0l7tI4uDipiglLmB1lFGbaEAPKLPP6IVmUTbjpBDeMDdjplpU_1yFotybDcGHFBQvJYp62ebsWpGVpTStEkS9Xi6E4Wu2SQT8tJGGattFKFJmqLKdm91YXhs7eaDcMc8UBVxZzK8XIxAlpFA_KkQiSDuxNjYTzW1IKQevEpJUnaY8o083JbKurTnBBvam5UldTWT6wVi9Eg9FisDubqgQIR9TxYFn3C3NKAhtVqRdUZyYoFU2a0jeRokkUZhN7kgwLqR7SRjUzY4u9uQd4i_NfYC56h_E3OP8ZmofIym4rf4ZckWJupbpgZGZuZ0uYonyBdxh4icdInuEtHmJpKa0nr0g2r9hLRlakTAA=&g=w-w-w-w1HQHw-w2Xw-w3Xw-w2HQH

const downloadHtml = () => {
  const finalTemplate = templateContent.replace("[[URL]]", inputUrl.value);
  const blob = new Blob([finalTemplate], {
    type: "text/plain;charset=utf-8",
  });
  FileSaver.saveAs(blob, "index.html");

  // (REMOVED - as can just save the HTML, don't need to wrap in Zip)
  // const finalTemplate = templateContent.replace("[[URL]]", inputUrl.value);
  // const zip = new JSZip();
  // zip.file("index.html", finalTemplate);
  // zip.generateAsync({ type: "blob" }).then(function (zip) {
  //   FileSaver.saveAs(zip, "web.zip");
  // });
};
</script>
