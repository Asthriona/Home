<template>
  <v-app>
    <div class="background" :style="`background: ${background ? 'url(' + background + ')' : '#212529'}`">
    <v-main>
      <router-view :links="links" />
    </v-main>
    <!-- set custom background button -->
    <v-btn class="settings btn-img" @click="setCustomBackground()" icon>
      <v-icon>mdi-image</v-icon>
    </v-btn>
    <v-btn class="settings btn-addLinks" @click="addLink()" icon>
    <v-icon>mdi-plus</v-icon>
    </v-btn>
  </div>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    background: "",
    links: [
        {
          name: "Github",
          url: "https://github.com/Asthriona",
          icon: "mdi-github",
        },
        {
          name: "YouTube",
          url: "https://www.youtube.com",
          icon: "mdi-youtube",
        },
        {
          name: "Asthriona.com",
          url: "https://asthriona.com",
          icon: "mdi-web",
        },
        {
          name: "Asthriona.space",
          url: "https://asthriona.space",
          icon: "mdi-web",
        },
        {
          name: "Twitter",
          url: "https://twitter.com",
          icon: "mdi-twitter",
        },
        {
          name: "Anilist.co/asthriona",
          url: "https://anilist.co/user/Asthriona/",
          icon: "mdi-web",
        },
      ],
  }),
  created() {
    this.$vuetify.theme.dark = true;
    this.getBackground();
  },
  methods: {
    addLink() {
      const name = prompt("link Name");
      const url = prompt("link URL");
      const icon = prompt("link Icon");
      this.links.push({ name, url, icon });
      localStorage.setItem("links", JSON.stringify(this.links));
    },
    getBackground() {
      this.background = localStorage.getItem("background") || "";
    },
    setCustomBackground() {
      const background = prompt("背景画像のURLを入力してください");
      localStorage.setItem("background", background);
      return (this.background = background);
    },
    getSavedLinks() {
      const links = localStorage.getItem("links");
      if (!links) {
        return;
      }
      return (this.links = JSON.parse(links));
    }
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
.btn-addLinks {
  position: absolute;
  top: 10px;
  right: 50px;
  z-index: 100;
}
</style>
