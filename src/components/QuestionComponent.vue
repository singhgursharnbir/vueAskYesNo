<template>
  <div>
    <div class="row justify-content-center align-items-center">
      <div class="col-md-1 col-sm-12"></div>
      <div class="col-md-6 col-sm-12">
        <input
          type="text"
          v-model="question"
          v-on:input="$emit('set-input-value', question)"
          class="w-100 rounded p-2 font-weight-bold "
          placeholder="Type your question here"
        />
      </div>
      <div class="col-md-2 col-sm-12 pt-2 text-mobile-right">
        <button
          :disabled="isQuestion"
          class="btn-primary btn"
          title="Enter Question then click send"
          @click="$emit('fetch-image')"
        >
          Send
        </button>
      </div>
    </div>
    <div class="row mt-4 justify-content-center align-items-center">
      <div class="col-md-1 col-sm-12"></div>
      <div v-if="imageUrl" class="col-md-6 col-sm-12">
        <Loader v-if="loading" />
        <img
          class="w-100 img-responsive img-fluid height350 "
          :src="imageUrl"
          alt="giphy"
        />
      </div>
      <div v-else class="col-md-6 col-sm-12">
        <Loader v-if="loading" />
        <img
          class="w-100 img-responsive img-fluid height350 "
          src="https://media.giphy.com/media/l3DdrXKGnq2RdEnde/giphy.gif"
          alt="giphy"
        />
      </div>
      <div class="col-md-2 col-sm-12 ">
        <div class="row h-100 align-items-center">
          <div class="col-12">
            <h1
              v-if="yesOrNo"
              v-bind:class="{
                'text-success': yesOrNo == 'Yes',
                'text-danger': yesOrNo == 'No'
              }"
            >
              {{ yesOrNo }}
            </h1>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Loader from "./Loader";
export default {
  name: "QuestionComponent",
  components: {
    Loader
  },
  props: ["imageUrl", "yesOrNo", "questionValue", "loading"],
  data() {
    return {
      question: ""
    };
  },
  computed: {
    isQuestion() {
      if (this.questionValue) {
        return false;
      } else {
        return true;
      }
    }
  }
};
</script>

<style scoped>
.height350 {
  max-height: 350px;
}
</style>
