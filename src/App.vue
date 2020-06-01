<template>
  <div id="app">
    <Evaluation/>
  </div>
</template>

<script>
import Evaluation from '@/components/Evaluation.vue'

export default {
  components: {
    Evaluation
  }
}
</script>

<style>
  body {
    margin: 0;
  }
  #app {
    display: flex;
    height: 100vh;
    justify-content: center;
    align-items: center;
  }
</style>
