<template>
  <div class="rating">
    <label
      v-for="index of 10"
      :key="index"
      :class="{active: picked === index}"
    >
      {{ index }}
      <input
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
    }, 2500)
  }
}
</script>

<style scoped>
  .rating {
    display: inline-flex;
    align-items: center;
  }
  input {
    display: none;
  }
  label {
    font-family: 'Righteous', cursive;
    font-size: 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: border-box;
    width: 20px;
    height: 20px;
    margin: 5px;
    border: 1px solid black;
  }
  .active {
    border: none;
    background-color: #F5D734;
  }
</style>
