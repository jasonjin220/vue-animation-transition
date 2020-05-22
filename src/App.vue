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

        <transition :name="selectedTransition" mode="out-in">
          <div v-if="show" class="alert alert-warning my-2" key="warning">Warning div</div>
          <div v-else class="alert alert-danger my-2" key="danger">Danger div</div>
        </transition>

        <transition :name="selectedTransition">
          <div v-if="show" class="alert alert-info my-2">This is the first alert</div>
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
          <div
            style="width: 100%; height: 100px; background-color: lightgreen; margin-top: 5px; border-radius: 0 0 5px 5px; box-shadow: 1px 1px 2px #aaa"
            v-if="load"
          ></div>
        </transition>

        <hr />

        <select class="form-control" v-model="selectedComponent">
          <option value="app-danger-alert">Danger</option>
          <option value="app-success-alert">Success</option>
        </select>

        <div class="form-check form-check-inline">
          <input
            type="radio"
            class="form-check-input"
            name="selectComponentRadio"
            id="radioDangerComponent"
            value="app-danger-alert"
            v-model="selectedComponent"
          />
          <label class="form-check-label" for="radioDangerComponent">Danger</label>
        </div>

        <div class="form-check form-check-inline">
          <input
            type="radio"
            class="form-check-input"
            name="selectComponentRadio"
            id="radioSuccessComponent"
            value="app-success-alert"
            v-model="selectedComponent"
          />
          <label class="form-check-label" for="radioSuccessComponent">Success</label>
        </div>

        <transition :name="selectedTransition" mode="out-in">
          <component :is="selectedComponent" class="my-3"></component>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
import DangerAlert from "./components/DangerAlert.vue";
import SuccessAlert from "./components/SuccessAlert.vue";

export default {
  components: {
    "app-danger-alert": DangerAlert,
    "app-success-alert": SuccessAlert
  },

  data() {
    return {
      show: false,
      load: true,
      selectedTransition: "fade",
      elementWidth: 100,
      selectedComponent: "app-success-alert"
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
      this.elementWidth = 0;
      el.style.width = this.elementWidth + "px";
    },

    enter(el, done) {
      console.log("enter()");

      let round = 1;

      const interval = setInterval(() => {
        el.style.width = this.elementWidth + round * 10 + "px";
        round++;
        if (round > 30) {
          clearInterval(interval);
          done(console.log("enter.done()"));
        }
      }, 20);
    },

    afterEnter(el) {
      console.log("afterEnter()");
    },

    enterCancelled(el) {
      console.log("enterCancelled()");
    },

    beforeLeave(el) {
      console.log("beforeLeave()");
      this.elementWidth = 300;
      el.style.width = this.elementWidth + "px";
    },

    leave(el, done) {
      console.log("leave()");

      let round = 1;

      const interval = setInterval(() => {
        el.style.width = this.elementWidth - round * 10 + "px";
        round++;
        if (el.style.width == "0px") {
          clearInterval(interval);
          done(console.log("leave.done()"));
        }
      }, 10);
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
