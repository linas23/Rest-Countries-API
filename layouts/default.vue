<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="title" to="/">{{title}}</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text @click="changeMode" id="fknbtn">
        <v-icon left>mdi-moon-waning-crescent</v-icon>
        {{mode}} mode
      </v-btn>
    </v-app-bar>
    <v-content class="px-5">
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-content>

    <v-footer tag="footer">
      <span>
        &copy; 2019 Made with
        <v-icon color="red">mdi-heart</v-icon>
        <span>by Sanil Desemaru</span>
      </span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      darkMode: false,
      title: "Where in the world"
    };
  },
  computed: {
    mode() {
      return this.darkMode ? "dark" : "light";
    }
  },
  methods: {
    changeMode() {
      const header = document.querySelector("header");
      const content = document.querySelector("main");
      const footer = document.querySelector("footer");
      const btn = document.querySelector("#fknbtn");
      let themes = [header, content, footer];
      this.darkMode = !this.darkMode;
      if (this.darkMode) {
        btn.style.color = "white";
        this.darkModeOn(themes);
      } else {
        btn.style.color = "black";
        this.lightModeOn(themes);
      }
    },
    darkModeOn(themes) {
      themes.forEach(el => {
        el.style.background = "#171223";
        el.style.color = "white";
      });
    },
    lightModeOn(themes) {
      themes.forEach(el => {
        el.style.background = "white";
        el.style.color = "#171223";
      });
    }
  }
};
</script>
<style>
html {
  scroll-behaviour: smooth;
}
</style>