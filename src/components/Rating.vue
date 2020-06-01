<template>
  <div class="rating">
    <label
      class="point"
      v-for="index of 10"
      :key="index"
      :class="{active: picked === index}"
    >
      {{ index }}
      <input
        class="point__input"
        v-model="picked"
        @click="update"
        :value="index"
        type="radio"
        name="rating"
      >
    </label>
  </div>
</template>

<script>
import debounce from 'lodash.debounce'

export default {
  props: {
    rating: Number
  },
  data () {
    return {
      picked: this.rating
    }
  },
  methods: {
    update: debounce(function () {
      this.$emit('update-rating', this.picked)
    }, 2000)
  }
}
</script>

<style scoped>
  .rating {
    display: inline-flex;
    align-items: center;
    margin-bottom: 69px;
    padding-right: 13px;
  }
  .point__input {
    display: none;
  }
  .point {
    font-family: 'Righteous', cursive;
    font-size: 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: border-box;
    width: 24px;
    height: 22px;
    margin: 3.3px;
    cursor: pointer;
    border: 1px solid black;
  }
  .active {
    border: none;
    background-color: #f5d734;
  }
</style>
