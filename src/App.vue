<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Animations</h1>

        <button @click="toggleAlert" class="btn btn-primary">Show alert</button>

        <transition name="fade">
          <div v-if="show" class="alert alert-info my-2">This is a faded alert</div>
        </transition>

        <transition name="slide" type="animation">
          <div v-if="show" class="alert alert-info my-2">This is a slided and faded alert</div>
        </transition>

        <transition name="slide" type="animation" appear>
          <div v-if="show" class="alert alert-info my-2">This is a slided, faded and onLoad alert</div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return { show: true };
  },

  methods: {
    toggleAlert() {
      this.show = !this.show;
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
  transition: opacity 3s;
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
