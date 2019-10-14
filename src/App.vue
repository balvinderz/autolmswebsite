<template>
  <v-app>
    <v-app-bar app dark color="#000">
      <v-toolbar-title class="headline text-uppercase">
        <span>Auto LMS</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <Home />
    </v-content>
  </v-app>
</template>

<script>
import Home from "./components/Home";

export default {
  name: " ",
  components: {
    Home
  },
  data: () => ({
    //
  })
};
</script>
