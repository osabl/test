<template>
  <div>
    <h2 class="title">Would you recommend our service to others?</h2>
    <Rating
      :rating="rating"
      @update-rating="$emit('update-rating', $event)"
    />
  </div>
</template>

<script>
import Rating from '@/components/Rating.vue'

export default {
  components: {
    Rating
  },
  props: {
    rating: Number
  }
}
</script>

<style scoped>
  .title {
    font-family: 'Roboto', sans-serif;
    font-size: 26px;
    font-weight: 700;
    line-height: 32px;
    margin: 70px 0 5.8px 0;
  }
</style>
