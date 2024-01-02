<template>
  <div id="app">
    <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>
    <section v-else>
      <div v-if="loading">
        <div class="spinner-border text-primary" role="status">
          <span class="sr-only">Loading...</span>
        </div>
      </div>
      <div v-else class="d-flex justify-content-center align-items-center vh-100">
        <div class="h-50">
          <Wordle v-bind:word="word"/>
          <div class="world-link">
            <a href="https://www.nytimes.com/games/wordle/">
              <img src="/src/assets/wordle-icon.svg"
              class="img-thumbnail"
              title="Play Wordle" />
            </a>
          </div>
        </div>
        <div class="note">
          New starting word is generated daily at 00:00 UTC 
        </div>
      </div>
    </section>
  </div>
</template>

<script>

import axios from "axios";
import Wordle from "./components/Wordle.vue";

export default {
    name: "App",
    data() {
        return {
            word: "",
            errored: false,
            loading: true
        };
    },
    created() {
        axios.get("https://api.masterbranch.io/b/wd")
        .then(response => (this.word = response.data.data))
        .catch(error => {
          console.log(error)
          this.errored = true;
        })
        .finally(() => (this.loading = false));
    },
    components: { Wordle }
};

</script>

<style>

body {
  background: #f6f6f6;
}

.spinner-border {
  position: fixed;
  z-index: 1;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  width: 50px;
  height: 50px;
  margin: auto;
}

.sr-only {
  display: none;
}

.note {
  font-size: 0.65rem;
  color: gray;
  bottom: 0;
  position: absolute;
}

.world-link {
  margin-top: 20%;
  transform: translateX(-50%);
  position: absolute;
  left: 50%;
}

</style>
