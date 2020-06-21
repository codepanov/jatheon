<template>
  <div class="s-wrapper">
    <div class="s-selected disabled" ref="selected">
      {{ payload.message }}
      <img src="@/assets/icn-arrow-down.svg" alt="Arrow" ref="image">
    </div>
  </div>
</template>

<script>
export default {
  props: {
    payload: {
      type: Object,
      required: true
    }
  },
  mounted() {
    let refs = [this.$refs.selected, this.$refs.image]
    refs.map(ref => ref.addEventListener('mousedown', function(e){ e.preventDefault() }, false))
  }
}
</script>

<style>
  .disabled {
    background: lightgrey;
    opacity: 0.25;
  }
</style>