<template>
  <div>
    <h2>Please specify</h2>
    <Multiselect :selection="selection" :selected="specify" @update-selected="$emit('update-selected', $event)"/>
  </div>
</template>

<script>
import Multiselect from '@/components/Multiselect.vue'

export default {
  components: {
    Multiselect
  },
  props: {
    specify: Array
  },
  data () {
    return {
      selection: [
        'one',
        'two',
        'three',
        'four',
        'five',
        'six',
        'seven'
      ]
    }
  }
}
</script>
