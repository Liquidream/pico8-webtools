<template>
  <v-app>
    <v-main>
      <Main/>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import Main from './components/Main.vue'

export default defineComponent({
  name: 'App',

  components: {
    HelloWorld,
    Main
  },

  data () {
    return {
      //
    }
  },
})
</script>
