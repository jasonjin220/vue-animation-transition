<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mx-auto my-4">
        <h3 class="text-center text-dark">The Super Quiz</h3>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mx-auto">
        <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question'"></component>
      </div>
    </div>
  </div>
</template>


<script>
import Question from "./Question.vue";
import Answer from "./Answer.vue";

export default {
  components: {
    "app-question": Question,
    "app-answer": Answer
  },

  data() {
    return {
      mode: "app-question"
    };
  },

  methods: {
    answered(isCorrect) {
      if (isCorrect) {
        this.mode = "app-answer";
      } else {
        this.mode = "app-question";
        alert("Wrong, try again!");
      }
    }
  }
};
</script>

<style  scoped>
</style>