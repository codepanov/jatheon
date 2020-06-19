<template>
  <div id="audit">
    <Selector />
  </div>
</template>

<script>
import Selector from '@/components/Selector.vue'

export default {
  components: {
    Selector
  }
}
</script>

<style scoped>
  #audit {
    display: flex;
    justify-content: center;
    box-sizing: border-box;
    height: 100vh;
    width: 100%;
    border: 1px solid green;
  }
</style>