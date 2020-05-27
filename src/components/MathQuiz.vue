<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mx-auto my-4">
        <h3 class="text-center text-dark">The Math Quiz</h3>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mx-auto">
        <transition name="flip" mode="out-in">
          <component :is="mode" @answered="answered" @confirmed="mode = 'app-question'" />
        </transition>
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
.flip-enter {
  transform: rotateY(0deg);
}

.flip-enter-active {
  animation: flip-in 0.1s ease-out forwards;
}

.flip-leave {
  /* transform: rotateY(0deg); */
}

.flip-leave-active {
  animation: flip-out 0.1s ease-out forwards;
}

@keyframes flip-out {
  from {
    transform: rotateY(0deg);
  }
  to {
    transform: rotateY(90deg);
  }
}

@keyframes flip-in {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}
</style>