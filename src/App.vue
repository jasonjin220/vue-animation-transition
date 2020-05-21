<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Animations</h1>

        <select class="form-control form-control-sm" v-model="selectedTransition">
          <option value="fade">Fade</option>
          <option value="slide">Slide</option>
        </select>
        <br />
        <button @click="toggleAlert" class="btn btn-primary form-control">Show alerts</button>

        <transition :name="selectedTransition">
          <div v-if="show" class="alert alert-info my-2">This is a faded alert</div>
        </transition>

        <transition :name="selectedTransition" mode="out-in">
          <div
            v-if="show"
            class="alert alert-warning my-2"
            key="warning"
          >This is a slided and faded alert</div>
          <div v-else class="alert alert-danger my-2" key="danger">This is a slided and faded alert</div>
        </transition>

        <hr />

        <transition enter-active-class="animated bounce" leave-active-class="animated swing">
          <div v-if="show" class="alert alert-info my-2">This is an animated bounce swing div</div>
        </transition>

        <hr />

        <div
          v-if="show"
          :class="animationHeadShake"
          class="alert alert-info my-2"
        >This is animated alert</div>

        <hr />

        <button class="btn btn-success form-control" @click="load = !load">Load Remove Element</button>
        <br />
        <br />
        <transition
          @before-enter="beforeEnter"
          @enter="enter"
          @after-enter="afterEnter"
          @enter-cancelled="enterCancelled"
          @before-leave="beforeLeave"
          @leave="leave"
          @after-leave="afterLeave"
          @leave-cancelled="leaveCancelled"
          :css="false"
        >
          <div style="width: 100px; height: 100px; background-color: lightblue" v-if="load"></div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: false,
      load: true,
      selectedTransition: "fade"
    };
  },

  computed: {
    animationHeadShake() {
      return "animated infinite headShake slow";
    }
  },

  methods: {
    toggleAlert() {
      this.show = !this.show;
    },

    beforeEnter(el) {
      console.log("beforeEnter()");
    },

    enter(el, done) {
      console.log("enter()");
      done(console.log("enter.done()"));
    },

    afterEnter(el) {
      console.log("afterEnter()");
    },

    enterCancelled(el) {
      console.log("enterCancelled()");
    },

    beforeLeave(el) {
      console.log("beforeLeave()");
    },

    leave(el, done) {
      console.log("leave()");
      done(console.log("leave.done()"));
    },

    afterLeave(el) {
      console.log("afterLeave()");
    },

    leaveCancelled(el) {
      console.log("leaveCancelled()");
    }
  }
};
</script>

<style>
.fade-enter {
  opacity: 0;
}

.fade-enter-active {
  transition: opacity 0.5s;
}

.fade-leave {
  /* opacity: 1; */
}

.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
}

.slide-enter {
  opacity: 0;
  /* transform: translateY(20px) */
}

.slide-enter-active {
  animation: slide-in 1s ease-out forwards;
  transition: opacity 1s;
}

.slide-leave {
}

.slide-leave-active {
  animation: slide-out 1s ease-out forwards;
  transition: opacity 1s;
  opacity: 0;
}

@keyframes slide-in {
  from {
    transform: translateY(5px);
  }
  to {
    transform: translateY(0px);
  }
}

@keyframes slide-out {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(10px);
  }
}
</style>
