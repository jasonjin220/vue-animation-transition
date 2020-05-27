<template>
  <div class="btn-group" role="group" aria-label="Choose Part">
    <button
      @click="togglePart(1)"
      type="button"
      :class="{ active: (part == 1) }"
      class="btn btn-light"
    >Part I</button>
    <button
      @click="togglePart(2)"
      type="button"
      :class="{ active: (part == 2) }"
      class="btn btn-light"
    >Part II</button>
  </div>
</template>

<script>
export default {
  props: {
    part: Number
  },

  methods: {
    togglePart(value) {
      this.$emit("toggle-part", value);
    }
  }
};
</script>

<style  scoped>
</style>