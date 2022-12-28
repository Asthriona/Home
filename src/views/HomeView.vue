<template>
  <div class="home">
    <v-container>
      <v-row align="center" justify="center">
        <v-col cols="12" class="intro" align="center" justify="center">
          <h1><span @click="updateUsername()">{{ username }}</span>, {{ time.line }}</h1>
          <h2>
            現在の時刻は<span class="time">{{ time.clock }}</span>です <br />
            あなたの場所は東京、日本です
          </h2>
        </v-col>
        <v-col cols="6" class="google-search" align="center" justify="center">
          <!-- Form Redirect google Search -->
          <!-- TODO: Move to dedicated comp -->
          <!-- DONE: Set to Vue element with JavaScript -->
          <!-- TODO: Clear search once clicked -->
          <v-form @submit="googleSearch()">
            <v-text-field
              v-model="search"
              label="Google Search"
              placeholder="Search"
              prepend-inner-icon="mdi-magnify"
              @keyup.enter="googleSearch()"
            ></v-text-field>

          </v-form>
        </v-col>
      </v-row>
        <v-row align="center" justify="center">
          <!-- Usefull links -->
          <!-- Github, Youtube, Gmail, Asthriona.com, Asthriona.space, Tweetdeck, Anilist.co/asthriona -->
          <v-col cols="1" v-for="link in links" :key="link.name" align="center" justify="center">
            <v-btn :href="link.url" icon>
              <v-icon>{{ link.icon }}</v-icon>
            </v-btn>
            <br />
            <a :href="link.url" target="_blank" rel="noopener noreferrer">{{ link.name }}</a>
          </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
// import axios from 'axios'
export default {
  name: "home-page",
  props: ["links"],
  data() {
    return {
      meteo: {},
      username: "",
      time: {},
      search: "",
    };
  },
  created() {
    this.getUsername();
    this.getLocalTime();
    this.updateClock();
  },
  methods: {
    // get username from local storage
    getUsername() {
      const username = localStorage.getItem("username");
      if (!username) {
        // Prompt the user with an alert asking for their username in japanese
        const username = prompt("お名前を教えてください");
        // Save the username to local storage
        localStorage.setItem("username", username);
      }
      return (this.username = `${username}さん`);
    },
    // get local time
    getLocalTime() {
      const time = new Date();
      if (time.getHours() < 12) {
        this.time.line = "おはようございます!";
        return (this.time.clock = time.toLocaleTimeString());
      }
      if (time.getHours() >= 12 && time.getHours() < 18) {
        this.time.line = "こんにちは!";
        return (this.time.clock = time.toLocaleTimeString());
      }
      if (time.getHours() >= 18) {
        this.time.line = "こんばんは!";
        return (this.time.clock = time.toLocaleTimeString());
      }
      if (time.getHours() >= 22) {
        this.time.line = "おやすみなさい!";
        return (this.time.clock = time.toLocaleTimeString());
      }
    },
    // Update clock every 1 second
    updateClock() {
      setInterval(() => {
        const time = new Date();
        this.time.clock = time.toLocaleTimeString()
        // get document element by class name "time"
        const clock = document.getElementsByClassName("time");
        // set the innerHTML of the clock to the current time
        clock[0].innerHTML = this.time.clock;
      }, 1000);
    },
    // redirect to google search
    googleSearch() {
      window.location.href = `https://www.google.com/search?q=${this.search}`;
    },
    // update username
    updateUsername() {
      const username = prompt("お名前を教えてください");
      localStorage.setItem("username", username);
      return (this.username = `${username}さん`);
    },
  },
};
</script>

<style scoped>
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 80vh;
}

</style>
