<template>
  <v-app>
    <div class="background" :style="`background: ${background ? 'url(' + background + ')' : '#212529'}`">
    <v-main>
      <router-view />
    </v-main>
    <!-- set custom background button -->
    <v-btn class="btn-img" @click="setCustomBackground()" icon>
      <v-icon>mdi-image</v-icon>
    </v-btn>
  </div>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    background: "",
  }),
  created() {
    this.$vuetify.theme.dark = true;
    this.getBackground();
  },
  methods: {
    getBackground() {
      this.background = localStorage.getItem("background") || "";
    },
    setCustomBackground() {
      const background = prompt("背景画像のURLを入力してください");
      localStorage.setItem("background", background);
      return (this.background = background);
    },
  },
};
</script>

<style>
.background {
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  height: 100vh;
}
.btn-img {
  position: absolute;
  top: 10px;
  right: 10px;
  z-index: 100;
}
</style>
