<template>
  <div id="app" class="container">
    <div class="row h-100">
      <div class="col-md-12 col-sm-8 m-4">
        <Header />
        <Description />
        <QuestionComponent
          v-bind:yesOrNo="yesOrNo"
          v-bind:imageUrl="imageUrl"
          v-bind:questionValue="questionValue"
          v-bind:loading="loading"
          v-on:fetch-image="getRandom"
          v-on:set-input-value="setInputValue"
        />
        <div class="row mt-2">
          <Footer />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";

import Footer from "./components/Footer.vue";
import Header from "./components/Header.vue";
import QuestionComponent from "./components/QuestionComponent";
import Description from "./components/Description";

export default {
  name: "App",
  components: {
    Footer,
    Header,
    QuestionComponent,
    Description
  },
  data() {
    return {
      active: false,
      yesOrNo: "",
      imageUrl: "",
      questionValue: "",
      loading: false
    };
  },
  methods: {
    getRandom() {
      this.imageUrl = "";
      this.loading = true;
      let arr = ["Yes", "No"];
      setTimeout(() => {
        let thisRandom = arr[Math.floor(Math.random() * arr.length)];
        this.yesOrNo = thisRandom;
        this.fetchImage(thisRandom);
      }, 1000);
    },
    fetchImage(thisRandom) {
      this.loading = true;
      fetch(
        `https://api.giphy.com/v1/gifs/search?q=${thisRandom}&api_key=R1xlrTlzaEYYQvoJVDEmft0ortyXKIP1`
      )
        .then(res => res.json())
        .then(photoData => {
          let dataArray = photoData.data;
          let pickRandom =
            dataArray[Math.floor(Math.random() * dataArray.length)];
          this.imageUrl = pickRandom.images.original.url;
          this.loading = false;
        });
    },
    setInputValue(question) {
      this.questionValue = question;
    }
  }
};
</script>

<style>
html,
body {
  margin: 0;
  height: 100%;
  background-color: #343a40 !important;
}
@media (max-width: 767px) {
  .text-mobile-right {
    text-align: right;
  }
}

/* loader css */
.center {
  z-index: 1000;
  margin: auto;
  width: 50%;
  max-width: 400px;
  min-width: 150px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 20px;
}
div.loader {
  font-size: 100px;
  color: black;
  text-align: center;
}

.loaded {
  font-size: 1.2em;
  font-weight: bold;
  margin-bottom: 10px;
}
</style>
