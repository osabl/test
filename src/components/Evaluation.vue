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
import gql from 'graphql-tag'

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
    this.addRecommendation()
  },
  methods: {
    addRecommendation () {
      const newRecommendation = {
        rating: 0,
        specify: '[]',
        message: ''
      }

      this.$apollo.mutate({
        mutation: gql`mutation ($object: recommendations_insert_input!) {
          insert_recommendations_one(object: $object) {
            id
            rating
            specify
            message
          }
        }`,
        variables: {
          object: newRecommendation
        }
      }).then(response => {
        const { id, rating, specify, message } = response.data.insert_recommendations_one

        this.recommendation = {
          id,
          rating,
          specify: JSON.parse(specify),
          message
        }
      })
        .catch(err => console.log(err))
    },
    updateRating (value) {
      this.recommendation.rating = value
      this.$apollo.mutate({
        mutation: gql`mutation ($id: Int!, $rating: Int) {
          update_recommendations(_set: {rating: $rating}, where: {id: {_eq: $id}}) {
            returning {
              id
            }
          }
        }`,
        variables: {
          id: this.recommendation.id,
          rating: value
        }
      })
      this.nextPage()
    },
    updateSelected (value) {
      this.recommendation.specify = value
      this.$apollo.mutate({
        mutation: gql`mutation ($id: Int!, $specify: String) {
          update_recommendations(_set: {specify: $specify}, where: {id: {_eq: $id}}) {
            returning {
              id
            }
          }
        }`,
        variables: {
          id: this.recommendation.id,
          specify: JSON.stringify(value)
        }
      })
    },
    updateMessage (value) {
      this.recommendation.message = value
      this.$apollo.mutate({
        mutation: gql`mutation ($id: Int!, $message: String) {
          update_recommendations(_set: {message: $message}, where: {id: {_eq: $id}}) {
            returning {
              id
            }
          }
        }`,
        variables: {
          id: this.recommendation.id,
          message: value
        }
      })
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
    width: 700px;
    text-align: center;
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16);
  }
</style>
