<template>
  <form class="evaluation">
      <Recommendation
        v-if="currentPage === 'recommendation'"
        :rating="recommendation.rating"
        @update-rating="updateRating"
      />
      <Specify
        v-else-if="currentPage === 'specify'"
        :selected="recommendation.specify"
        @update-selected="updateSelected"
        @prev="prevPage"
        @next="nextPage"
      />
      <Message
        v-else-if="currentPage === 'message'"
        @update-message="updateMessage"
        @prev="prevPage"
        @close="close"
      />
    </form>
</template>

<script>
import Recommendation from '@/components/Recommendation.vue'
import Specify from '@/components/Specify.vue'
import Message from '@/components/Message.vue'

export default {
  components: {
    Recommendation,
    Specify,
    Message
  },
  data () {
    return {
      recommendation: {},
      pages: ['recommendation', 'specify', 'message'],
      currentPage: 'recommendation'
    }
  },
  beforeMount () {
    this.recommendation = {
      userId: 123,
      rating: 5,
      specify: ['one', 'two', 'three', 'seven'],
      message: ''
    }
  },
  methods: {
    updateRating (value) {
      this.recommendation.rating = value
      this.nextPage()
    },
    updateSelected (value) {
      this.recommendation.specify = value
    },
    updateMessage (value) {
      this.recommendation.message = value
    },
    nextPage () {
      const nextIndex = this.pages.indexOf(this.currentPage) + 1

      if (nextIndex < this.pages.length) {
        this.currentPage = this.pages[nextIndex]
      }
    },
    prevPage () {
      const prevIndex = this.pages.indexOf(this.currentPage) - 1

      if (prevIndex >= 0) {
        this.currentPage = this.pages[prevIndex]
      }
    },
    close () {
      this.currentPage = []
    }
  }
}
</script>

<style scoped>
  .evaluation {
    text-align: center;
    width: 700px;
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16);
  }
</style>
