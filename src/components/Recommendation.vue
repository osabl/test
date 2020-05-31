<template>
  <div>
    <h2>Would you recommend our service to others?</h2>
    <Rating :rating="rating" @update-rating="$emit('update-rating', $event)"/>
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
