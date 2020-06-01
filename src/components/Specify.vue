<template>
  <div>
    <h2 class="title">Please specify</h2>
    <Multiselect
      :selection="selection"
      :selected="selected"
      @update-selected="$emit('update-selected', $event)"
    />
    <button class="btn btn-prev" @click="$emit('prev')"></button>
    <button class="btn btn-next" @click="$emit('next')"></button>
  </div>
</template>

<script>
import Multiselect from '@/components/Multiselect.vue'

export default {
  components: {
    Multiselect
  },
  props: {
    selected: Array
  },
  data () {
    return {
      selection: [
        'simple to use',
        'easy to understand',
        'fair price',
        'good customer support',
        'real time capabilities',
        'site speed',
        'happy to use',
        'user interface'
      ]
    }
  }
}
</script>

<style scoped>
  .title {
    font-family: 'Roboto', sans-serif;
    font-size: 26px;
    font-weight: 700;
    line-height: 32px;
    margin-top: 38px;
    margin-bottom: 17px;
  }
  .btn {
    width: 70px;
    height: 50px;
    margin: 37px 30px;
    cursor: pointer;
    border: none;
    background-color: #8d9599;
  }
  .btn-prev {
    background-image: url(../assets/arrow.svg);
    background-repeat: no-repeat;
    background-position: center;
  }
  .btn-next {
    transform: rotate(180deg);
    background-image: url(../assets/arrow.svg);
    background-repeat: no-repeat;
    background-position: center;
  }
</style>
